Tmux 8 hours per day. (use case)


Main part.
In this article, I would like to share my vision, how to make terminal work for you, feel comfortable in this black rectangle with a blinking cursor.
Many of you have heard about different shells like bash, zshell, fish. You can customize prefix for command line in the way it can show git branch, current directory, local or remote computer name.

You can do a useful setup that will improve your productivity, will help you to operate with the terminal in an effective way.
You can run a program and see the logs of execution of this program, almost like in the Matrix movie.
Yes, but we are talking about 1 screen. What if you want to run another program in parallel?
Modern terminal emulators like iTerm have their own window manager.
So with it, you can create vertical and horizontal splits, you can create as many tabs as you want. This is pretty helpful. Now you can run 3, 5, 10 commands at the same time.
You can have all your commands in the same terminal instead of open 10 terminal windows.
But what if you want terminal emulator agnostic solution. You want to be comfortable in any terminal emulator.
Here it goes. Old good tmux will help you.
Tmux stands for Terminal Multiplexer. 
This is a tiny application that aims to help you to organize all your terminal windows and panes (see below for details).

Personally, I use tmux to organize my working environment and focus on the current task, and have all necessary logs, tests output, docker images, IDE right below my fingers. 
It reduces the time to navigate to any part of my working environment.

The first concept which will help us to understand how to use tmux is `Session`.

The Session is the root working block of tmux. You can create a session, detach from it and attach back to it to restore exactly the same state when you were detached from. 
It allows you to setup your working process according to your needs. 
Session is your container for windows.

What is the window in the scope of tmux, you can ask?
A window is a group of your command lines. You can easily give a logical name to the window which will combine `Panes` with running commands.
And the `Pane` is the last tmux term, I promise :)
The `Pane` is actually the black rectangle with the command line we were talking about at the beginning of this article.

So it gives you a nice tool to organize your terminal workspace. 
Simply type in terminal `tmux new -s dashboards` and you have a session with the name `dashboards'. 
Inside this session you can have windows called as follow: 0:'docker', 1:'backends', 2:'frontends'. Tmux creates a new window and prepends it with a digit for easy navigation.
Press `Ctrl+b c` to create new window.
'docker' window can have as many `panes` as you want, but we can have a simple vertical split where you can run some docker image without `-d` option to have logs from running docker container and leave another pane
to be ready for any other docker commands, like `docker ps -a` so on.
To make a vertical split you can type Ctrl+b %, for horizontal split Ctrl+b " accordingly.( Most not intuitive key binding from 50 existing )
`backends` window will have 6 panes, 3 horizontal and 2 vertical. On each of the pane, we can execute the command which will run a specific backend microservice. In this way, you can have separate logs per microservice.
And the last window called `frontends` will have 3 split panes, with 3 running frontend processes.

Ok, we have setup, what then?

How to navigate?
It is pretty easy.

Tmux has default special key binding which allows to execute tmux commands.
For example, to switch from window 0 to window 2 you need to press Ctrl+b 2 and you will see a window with 3 frontends running.
Just simple as press default key binding Ctrl+b and number of the window.
Also, it is possible to navigate to the next window with Ctrl+b n, and previous Ctrl+b p.
Who is familiar with vim can find it logical to use j,k,h,l for navigation between panes Ctrl+b [j, k, h, l] will navigate between panes down, up, left, right accordingly.
What if the iTerm application crashes?
Not a problem at all, because tmux session is a special kind of process that still run even if the terminal crashes.
So simply run terminal again, type `tmux attach -t dashboards` and you will see the same setup as it was before the terminal crash.
Is it possible with iTerm windows and tabs? No, it isn't. 
Tmux solves this problem.

Conclusion.
Actually, it is pretty easy to start to work with tmux. Don't be afraid of hotkeys, they are intuitive and simple. You can always type Ctrl+b ? to list them all. (Press `q` to exit from key bindings help screen)
I hope you read this line :) as a bonus, I will give you key binding to detach from the session: Ctrl+b d.
Here you can find a lot of useful key bindings and commands ('Ctrl+b :' will allow you to type tmux command): https://tmuxcheatsheet.com
To kill tmux session you can press 'Ctrl+b :' and type `:kill-session`.
Good luck!