#Tmux 8 hours per day. Tmux terms. 

  This is the second article in series of articles about tmux. You can find Intro here.

  In this article, I would like to share my vision, how to make terminal work for you, feel comfortable in this black rectangle with a blinking cursor.
    
  Many of you have heard about different shells like bash, zshell, fish. You can customize prefix for command line in the way it can show git branch, current directory, local or remote computer name. You can do a useful setup that will improve your productivity, will help you to operate with the terminal in an effective way. You can run a program and see the logs of execution of this program, almost like in the Matrix movie. Yes, but we are talking about 1 screen. What if you want to run another program in parallel?

  Modern terminal emulators like iTerm have their own window manager. So with it, you can create vertical and horizontal splits, you can create as many tabs as you want. This is pretty helpful. Now you can run 3, 5, 10 commands at the same time. You can have all your commands in the same terminal instead of open 10 terminal windows. But what if you want terminal emulator agnostic solution? You want to be comfortable in any terminal emulator. Here it goes. Old good tmux will help you. 

  Tmux stands for Terminal Multiplexer. This is a tiny application that aims to help you to organize all your terminal windows and panes (see below for explanation).

  Personally, I use tmux to organize my working environment and focus on the current task, and have all necessary logs, tests output, docker images, IDE right below my fingers. It reduces the time to navigate to any part of my working environment.

##Tmux terminology.

  The first concept which will help us to understand how to use tmux is `Session`. The `Session` is the root working block of tmux. You can create a session, detach from it and attach back to it to restore exactly the same state when you were detached from. It allows you to setup your working process according to your needs. Session is your container for windows.

  What is the window in the scope of tmux, you can ask? A window is a group of your command lines. You can easily give a logical name to the window which will combine `Panes` with running commands.

  And the `Pane` is the last tmux term, I promise :) The `Pane` is actually the black rectangle with the command line we were talking about at the beginning of this article.

##Create your first session.

  Tmux gives you a nice tools to organize your terminal workspace. Simply type in terminal `tmux new -s awesome-session-name` and you have a session with the name `awesome-session-name`. Inside this session we will have windows called as follow: 0:'logs', 1:'backends', 2:'frontends'. Tmux creates a new window and prepends it with a digit for easy navigation.

##Create and rename windows.
  So let's rename our default first window which tmux created with new session. Just press `Ctrl+b ,` to see the rename prompt. Remove existing name with `delete` button on the keyboard (or with `Ctrl+w` on some systems) and type `logs`.

  Press `Ctrl+b c` to create new (second) window. Let's repeate rename step. Press `Ctrl+b ,` again and name it `backends`. Repeat the step for `frontends` window.

  As you can mention tmux by default starts to numerate windows from `0`. You can change this behaviour later by changing settings in `.tmux.conf` file.

##Navigation between windows.
  We already have 3 windows in tmux, so we need to be able to navigate between them. Tmux has special key-binding, which you actually already used. It is `Ctrl+b` also called `prefix`, which allows you to execute tmux commands and avoid a conflict with your OS or terminal emulator key-bindings. To navigate to the left window you need to press `Ctrl+b p` which stands for `previous`. To navigate to the right window just press `Ctrl+b n` which stands for `next` correspondly. Try this out and navigate to our first window ( 0: 'logs' ).
 
  Alternative way of navigation between windows is to use number assigned to the window by tmux. Just press `Ctrl+b 2` to navigate to `2: frontends` window. Now you can easily jump between windows sequentially or by specific number.

##Create panes
  Actually, you already have pane in every window you created. When you create new session, tmux actually creates session and default window with pane. You can use it immediately by typing any command in it. During creation of a new window we also have one pane created inside it. The next step (and final) is to create new panes inside the window.

  To make a vertical split you can type `Ctrl+b %`, for horizontal split `Ctrl+b "` accordingly. Most not intuitive key binding from 50 existing. 

  Lets navigate to 1: `backends` window and make a vertical split. So we will have 2 panes (left and right). We can do this using `Ctrl+b %` key-binding. Easy, right? Lets navigate between panes. 

  Are you familiar with vi, vim, neovim? Good news for you. Tmux uses the same h,j,k,l keys to navigate left, bottom, up, right. Just press `Ctrl+b h` to go left, and `Ctrl+b l` to go right. Now you can navigate between panes and windows. Similarly to windows jump by number, panes also has special jump mechanism. Press `Ctrl+b q` and tmux will highlight panes with assigned numbers. One downside of this approach that you need to quickly press number immediately after `Ctrl+b q`. I personally, do not often use this approach. Just let you know about an option.

##Bonus
  What if the iTerm (terminal emulator) application crashes? Not a problem at all, because tmux starts the server process that still run even if the terminal crashes. So simply run terminal again, type `tmux attach -t awesome-session-name` and you will see the same setup as it was before the terminal crashed/quited. Is it possible with iTerm windows and tabs? No, it isn't. Tmux solves this problem.

##Conclusion.
  Actually, it is pretty easy to start to work with tmux. Don't be afraid of hotkeys, they are intuitive and simple. You can always type `Ctrl+b ?` to list them all. (Press `q` to exit from key bindings help screen)

  I hope you read this line :) as a extra bonus, I will give you key binding to detach from the session: `Ctrl+b d`. Now you can attach to it again, remember `tmux attach -t ...` command?

  Here you can find a lot of useful key bindings and commands ('Ctrl+b :' will allow you to type tmux command): https://tmuxcheatsheet.com

  To kill tmux session you can press 'Ctrl+b :' and type `:kill-session`.


  Good luck!
