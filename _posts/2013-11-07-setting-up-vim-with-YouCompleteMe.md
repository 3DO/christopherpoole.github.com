---
layout: minimal_post
title: Setting up Vim with YouCompleteMe 
published: true 
comments: true
introduction: YouCompleteMe is basically better omni-completion for Vim; it finds matches in the current file you editing. It is great for both coding generally, and writing using LaTeX..
---

For best results, compile Vim from source, with Python enabled:

    hg clone https://vim.googlecode.com/hg/ vim
    cd vim/
    ./configure --enable-pythoninterp
    make -j8
    sudo make install

If you get an error saying you need a terminal library such as `ncurses`, install one, and try the above again:

    sudo apt-get install libncurses5-dev

We will let [vundle](https://github.com/gmarik/vundle) do all of the hard work for us in managing the installation and setup of YouCompleteMe. Put this inside your `~/.vimrc` file:

    syntax on
    set clipboard=unnamed
    set number
    set tabstop=4 shiftwidth=4 expandtab

    set nocompatible
    filetype off

    set rtp+=~/.vim/bundle/vundle/
    call vundle#rc()

    Bundle 'gmarik/vundle'
    Bundle 'Valloric/YouCompleteMe'

    filetype plugin indent on 

First download vundle:

    git clone https://github.com/gmarik/vundle.git ~/.vim/bundle/vundle

And then YouCompleteMe:

    git clone https://github.com/Valloric/YouCompleteMe.git ~/.vim/bundle/YouCompleteMe
    cd ~/.vim/bundle/YouCompleteMe
    git submodule update --init --recursive
    ./install.sh --clang-completer

Finally, run the following command in a terminal to finalise everythingi:

    vim +BundleInstall +qall


## Debian Users

If like me, you are running Debian stable, there are some hoops to jump though in order to satisfy the `GLIBC > 2.14` dependency.
We can pull the required package directly from `testing`, however we need to notify `apt` of exactly what distribution we are running. 

In `/etc/apt/apt.conf`:

    APT::Default-Release "stable";

In `/etc/apt/sources.list` put this line somewhere:

    deb http://ftp.iinet.net.au/debian/debian/ jessie main

The `apt.conf` file will protect us from installing files from `testing` ordinarily, however in making the `jessie` repository available, we can issue a one-liner to install the required package like this:

    sudo apt-get -t testing install libc6-dev 

That should be it.

