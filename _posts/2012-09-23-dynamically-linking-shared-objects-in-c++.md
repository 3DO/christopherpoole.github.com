---
layout: minimal_post
title: Dynamically Linking Shared Objects in C++
---

Dynamically linking shared objects (``*.so`` or ``*.dll``) at run time, as opposed to compile time in C is easy with <dlfcn.h>, this has been discussed all over the web by others.
The technique works in C++ too however, with a cavete; ISO C++ forbids casting between pointer-to-function and pointer-to-object, a limitation the user will invariably encounter when tring to load a object from the dynamically loaded library (the plugin).
Whilst casting between pointer-to-function and pointer-to-object is not defined for ISO C++, it is defined for POSIX so user code will compile, albiet with a warning.
Here we will quickly cover three techniques for either suppressing the warning or avoiding it with function redeclarations or some appropirate function pointer castings (one of which is the POSIX.1-2003 Technical Corrigendum 1 suggested work-around).
Further, we will create a template ``template<class T> class Plugin`` for loading objects of type ``T`` from a dynamically loaded library.

Dynamic Linking
---------------

Here we have the fundamental example usage of `<dlfcn.h>`.
First off, a main function opens a shared object using ``dlopen`` with ``RTLD_LAZY`` so we resolve symbols as the code is executed.
Using ``dlsym``, we find the function we want to execute in our shared object; finally, we execute the function in the shared object, and close it.

File ``main.cpp``:
{% highlight cpp %}
    #include <iostream>
    #include <dlfcn.h>

    typedef void (*func_t)();

    int main() {
        void * shared_object = dlopen("./test.so", RTLD_LAZY);
        func_t func = (func_t) dlsym(shared_object, "func");

        func();
        
        dlclose(shared_object);
    }
{% endhighlight %}

In the target function in the shared object we just need ``extern "C"`` to avoid mangling thereby allowing ``dlsynm`` to find function by its name.

File ``test.cpp``:
{% highlight cpp %}
    #include <iostream>

    extern "C" void func() {
        std::cout << "Called func in shared_object." << std::endl;
    }
{% endhighlight %}

When we compile main, we need to link against the ``dl`` (dynamic link) library as shown below.
The code should compile without errors, (however we will get a point-to-function cast warning mentioned previously), and when run ``Called func in shared_object.`` should be printed to the terminal:

{% highlight sh%}
    >> g++ -pedantic -fPIC -o example main.cpp -ldl
    main.cpp: In function ‘int main()’:
    main.cpp:9:55: warning: ISO C++ forbids casting
                   between pointer-to-function and
                   pointer-to-object [enabled by default]
    >> g++ -fPIC -shared -o test.so test.cpp
    >> ./example
    Called func in shared_object.
{% endhighlight %}

This is a very basic example without any sort of error checking during the loading of the shared object or symbol searching.
If the shared object or a symbol is not found, we will get a ``Segmentation fault``; we will incorperate some error checking later on.

Warning Suppression by Redeclaring ``dlsym``
--------------------------------------------

[Agram's Agnostic Agony](http://agram66.blogspot.com/2011/10/dlsym-posix-c-gimme-break.html) shows that a redeclaration of ``dlsym`` can make the warnings go away.
If you want a quick and easy fix for pre-existing code, this will do the trick::

{% highlight cpp %}
    #define dlsym __ 
    #include <dlfcn.h> 
    #undef dlsym 

    extern "C" void *(*dlsym(void *handle, const char *symbol))();
{% endhighlight %}

Casting the ``dlsym`` Return Type
---------------------------------

Whilst the author has not yet encoutered this, [toidinamaiblog](http://blog.toidinamai.de/en/programming/dlsym) suggests that the previous method may result in warning such as ``dereferencing type-punned pointer will break strict-aliasing rules``.
By casting the return type of dlsum, this waring can be avoid::

{% highlight cpp %}
    typedef hook_fn (*hook_dlsym_t)(void *, const char *);
    f = ((hook_dlsym_t)(dlsym))(h, "hook");
{% endhighlight %}


POSIX.1-2003 Technical Corrigendum 1 Work-around
------------------------------------------------

In an example on the [dlsym man page](http://linux.die.net/man/3/dlsym) (towards the bottom) we see that:

... the C99 standard leaves casting from "void \*" to a function pointer undefined. The assignment used below is the POSIX.1-2003 (Technical Corrigendum 1) workaround...

{% highlight cpp %}
    TargetObject* (*PluginEntry)();
    void (*PluginExit)(TargetObject*);

    void * plugin = dlopen("plugin.so", RTLD_LAZY);
    *(void **) (&PluginEntry) = dlsym(plugin, "create");
    *(void **) (&PluginExit) = dlsym(plugin, "destroy");
{% endhighlight %}

This methodology has been impemented using a simple template [here](https://github.com/christopherpoole/cppplugin).
