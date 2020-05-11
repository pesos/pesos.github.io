---
title: "Living in the Terminal"
tags: terminal linux
author: Anirudh H M
---

Many new Linux users have the same first question: Why is everything done on the terminal? Indeed, computer graphics have come a long way, and with flashy GUIs available on other operating systems, Linux seems prehistoric and daunting to many new users. However, anyone who's taken the effort to get comfortable with the terminal will tell you that it is almost always the faster, more efficient option. Just think of how much time can be saved by being able to do everything from one application! To make things easier, here's a list of nice terminal applications for various uses.

## Editors
Without getting into the [holy wars](https://en.wikipedia.org/wiki/Editor_war), both Emacs and Vim are great editor options for almost all programming (and non-programming) uses. Between the two, Vim is more lightweight, but Emacs is more feature-rich by default. However, both editors can be infinitely configured to your liking. Both editors come with extensive inbuilt documentation, as well as huge online communities. A word of advice: the default Emacs keybindings are known to be hard on the fingers, so if you're going for Emacs, try some of the nicer keybindings such as [evil-mode](https://www.emacswiki.org/emacs/Evil) or [god-mode](https://chrisdone.com/posts/god-mode/)

## File browsers
For experienced command-line users, file browsers may be seen as unnecessary software. However, it's often useful to have a visual representation of the directory structure, maybe with a preview of the files to get an idea of what it contains. And no, you don't need a graphical file manager for that. [Vifm](https://vifm.info/) and [ranger](https://github.com/ranger/ranger) are two excellent file browsers for the terminal, with full support for all file and folder actions, permissions management and previews. Both have vim-like keybindings, so if you invest the time in learning them once, you can use them here too!

## Music players
So you want to jam to some tunes while studying, and surely you can't do that on the terminal? Well, there are several options for listening to music from the terminal. [Mpd](https://www.musicpd.org/) and [MOC](http://moc.daper.net/) are great options, which have the added benefit of running a server in the background, so you can control your music from the keyboard hotkeys without opening the application. If that's not something you need, [cmus](https://cmus.github.io/) is a nice, non-server-based music player for the terminal. All of these players can read almost any format you throw at them, have support for playlist creation and much more! If you prefer streaming music, there's also a Spotify [CLI](https://github.com/pwittchen/spotify-cli-linux) you can use

## Email
Disclaimer: I've never used a terminal email application, but there are people who swear by them. They are most useful for people with lots of emails over multiple accounts, possibly with large attachments. Some great options include [mutt](http://www.mutt.org/), [notmuch](http://notmuchmail.org/) and [aerc](https://aerc-mail.org/). 

Now, you may wonder how an ancient-looking terminal application can compete with flashy new GUI applications with tons of features. The simple answer is that they don't compete at all! Most terminal applications follow what's known as the UNIX philosophy - **each application is designed to do a specific task _very_ well**, and nothing else. GUI applications, on the other hand, try to cram a large number of features into one application, often sacrificing performance (this is certainly not true for all applications, but a general trend nonetheless). As a result, you may need more than one terminal application to accomplish what you do with a single application right now, but it is almost guaranteed to be more performant (faster to start up and use) than your current solution.

Many people are also put off by the strange and complex keybindings found in many terminal applications. However, it's not as hard as it seems, for two reasons:

- Most of the keybindings are mnemonic (`d` for `delete`, `n` for `next`, `p` for `previous` and so on)
- Most keybindings are similar to other terminal applications
So here I present another advantage of moving to terminal applications - **you only have to learn the keybindings once!**

As a final example, here is my (simplified) workflow with terminal applications:

1. Music player starts in the background on boot, controllable with media keys on the keyboard (currently using MOC)
2. Open terminal and file browser (I use vifm)
3. Navigate to the project I'm currently working on
4. Open file to work on (I have a shortcut in vifm to open current file in vim)

The key takeaway here is that I can get all my work done on a single terminal. Since all my work related to the current project is likely to be in the same folder, I have no reason to constantly use a file browser to navigate to the right directory and open a file. Most of the common functions are accessible from the keyboard, so you never have to take your hands off it (great if you're a fast typist; if not, wouldn't hurt to learn)

All these applications can be customised immensely to fit your specific (functional and aesthetic) needs. They are all super fast to use, have huge communities behind them for support, and are just a joy to work with. Hope you find something useful here!
