---
layout: single
title:  Gear Up Vim
date:   2017-05-20
enableGiscus: true
# tags: vim
---
As a suspicious and paranoid guy, I always thought plugins will make vim run sluggish. And you'll get a hard time working on a different machine without those plugins. And I had some experience before that some plugins are really like toys that they might work in some cases but always come with a catch.

Last Friday, after so many years being a basic `vi` user, I finally decided to make my `Vim` more powerful by adding a bunch of plugins. It's mainly because watching other peoping use sublime or microsoft code really makes me want to switch my favorite editor. 

I first installed them on my Window 7 PC, tried and played around a bit and then my MBP. Here is the plugin I've added:

    Plugin 'VundleVim/Vundle.vim'
    Plugin 'tpope/vim-fugitive'
    Plugin 'scrooloose/nerdtree'
    Plugin 'plasticboy/vim-markdown'
    Plugin 'tpope/vim-surround'
    Plugin 'altercation/vim-colors-solarized'
    Plugin 'vim-airline/vim-airline'
    Plugin 'vim-airline/vim-airline-themes'
    Plugin 'pangloss/vim-javascript'
    Plugin 'scrooloose/syntastic'
    Plugin 'mattn/emmet-vim'
    Plugin 'ervandew/supertab'
    Plugin 'SirVer/ultisnips'
    Plugin 'honza/vim-snippets'
    Plugin 'valloric/youcompleteme'

I really like the `ultisnips`, `youcompleteme` and `vim-airline` plugins. For example, the snippet plugin allow me to insert html tag pairs quickly so I don't have to type them. This can really save me quite some time.

Then the `youcompleteme` is really doing an amazing job prompting me the candidate words as I type, much better than the default omnicomplete in terms of context relevance.

I wish I could post an gif here illustrating how they work out for me but unfortunately I don't have much time to playaround with it. But here are some resources that speak my mind.

1. [SnipMate](https://code.tutsplus.com/tutorials/vim-essential-plugin-snipmate--net-19356)
Although I use `ultisnips` and `vim-snippets`, this is really the tutorial that make my mind to add some snippet plugin. The reason I use `ultisnips` is that it's recommended by [vim-snippets](https://github.com/honza/vim-snippets) in the documentation. For those like me wondering why we need 2 plugins instead of 1, `vim-snippets` is a collection of code snippets for various programming launguages (html, css etc) while `ultisnips` is the engine that detect, insert, expand and autojump when you type a snippet name. Highly recommended.

2. [NERDTree](https://code.tutsplus.com/tutorials/vim-essential-plugin-nerdtree--net-19692)
Again from tutsplus. Really makes your vim more IDE like. Very visual and helpful if you work on projects based on a framework, which has multiple components to coordinate.

3. [VimAwesome](http://vimawesome.com/)
This is the ultimate ranking for vim plugins. If you're like me not sure which plugins to have, just follow the rankings. It won't disappoint you.

4. [vimcasts.org](http://vimcasts.org/)
I forgot which screencast I watched but this sites contain lots of good stuff.

5. [ultisnips and youcompleteme](http://stackoverflow.com/a/22253548/247807)
There's a little conflict between these 2 plugins and just I was about to be desperate, I find that SO answer making my day. `<tab>` works as normal and `ctrl-n` is used to go through other candidate which is totally fine to me.

Last, I must say that install those plugins on a mac is easier than on PC, especially the `youcompleteme` because you need compile it first.

P.S. Here is my complete [_vimrc](https://github.com/sandyleo26/dotfiles/blob/master/_vimrc) for your reference.
