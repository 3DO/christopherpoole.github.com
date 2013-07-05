---
layout: minimal_post
title: Setting up the ADT Bundle on Debian Wheezy (64bit) 
comments: True
introduction: Wheezy is the first Debian release to fully support multiarch. To get the Android emulator working, a correct multiarch setup is required.
---

The [ADT bundle](http://developer.android.com/sdk/index.html) is a single archive with everything you need to start developing for Android using eclipse, including eclipse itself and all of the NDK dependencies.
Device emulation is inherently 32bit, therefore on a 64bit machine a correct multiarch setup is required.
Previously the transitional package `ia32-libs` provided this support, as of Wheezy however, we need to explicitly add extra architectures we wish to use.

## Enabling multiarch
Add the `i386` architecture:

    sudo dpkg --add-architecture i386

Install `i386` dependencies: 

    sudo apt-get update
    sudo apt-get install ia32-libs

We also need `libncurses5` for our `i386` architecture:

    sudo apt-get install libncurses5:i386 

## Installing the ADT
With the `i386` dependencies met, this is the easy bit:

    1. [Download the ADT](http://developer.android.com/sdk/index.html) for your operating system
    2. Unzip it
    3. Run `<bundle directory>/eclipse/eclipse`

