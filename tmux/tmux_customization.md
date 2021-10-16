#Tmux 8 hours per day. Simple customization.

This is the third article in the "Tmux 8 hours per day series".
Here you can find "tmux Intro" and "tmux Terms" articles. 

Today I would like to show you how to customize tmux using .tmux.conf file.
Personally, I like minimalistic setup, so no much fancy things with date, time,
and battery status in tmux status line. 

If you didn't yet installed tmux, you can follow steps from the official tmux Github
page. [https://github.com/tmux/tmux/wiki/Installing]

I assume you already familiar with some command-line text editor.
I use 'neovim', but any other text editor will do the job.

Let's create new tmux session. We need it to be able to change tmux
configuration and see the results immediately.
$ tmux new -s customization

After fresh tmux installation you can find that ~/.tmux.conf file is
absent, so let's create it.
$ nvim ~/.tmux.conf

First useful key-binding is reload tmux config itself to apply changes.

Let's insert the following lines in the beginning of the .tmux.conf file.

```
# Easy source file
bind r source-file ~/.tmux.conf
```
Now you can save file and press 'Ctrl+b r' to reload it and see the changes.
Actually we do have nothing to observe as a change, so let's change background
color of the status line:
```
set -g status-style bg=#000000
```
bg - background color.
#000000 - is hex color code for the black color.
Save the file and press 'Ctrl+b r' to apply the changes.
Congratulations with your first custom tmux configuration.

Let's continue and add session name to the status line with custom background
and foreground colors:
```
set -g status-left "#[fg=#000000,bg=#61afef]#S#[fg=default,bg=default] "
```

fg - foreground color. Color of the session name.
bg - background color. Color of the background for the session name section.
#[fg=#xxxxxx,bg=#yyyyyy] - is the way to set the colors for the following text. In our case it is #S which represents tmux session name.
#xxxxxx and #yyyyyy - is hex color codes. #000000 for the black #ffffff for the white color.
#S - session name
Following '#[fg=default,bg=default]' restores colors. Last symbol is space is used to add separator between status-left section and the following section.

Next configurations are for the windows section:
```
set -g window-status-separator ' '
set -g window-status-format " #I #W#{?window_zoomed_flag,*,} "
set -g window-status-current-format "#[underscore,bold] #I #W#{?window_zoomed_flag,*,} "
```
#I - index of the window. As you remember from the previous article it is zero-based.
#W - window name.
{?window_zoomed_flag,*,} - appends symbol '*' to the window name if the window in zoomed state. See the explanation in the end of the article.
We have trailing spaces around our window-status-format to add extra air to the text.
For 'window-status-current-format' we do use the same trick with zoomed state,
but prepend it with `#[underscore,bold]` which adds extra emphasis to the
currently shown window.

Save the file and apply the changes.
That's it. Your simple and minimalistic tmux configuration is ready.
You can explore another examples of .tmux.conf from the internet, but you already have pretty solid base for it.

Bonus.
If you have more than 1 pane in the window, you can zoom-in active pane, so this pane will be expanded on the full screen. Using 'Ctrl+b z' key-binding you can zoom-in and zoom-out current pane, which gives you nice flexibility to focus on the current task. I use this functionality when edit some file and need to check in parallel something on terminal. So instead of opening new window, I actually open new pane and do the work. In this way I see both text editor and another pane at the same time. After I go back to edited file and press 'Ctrl+b z', so my file fulfill all the available space on the terminal. With our config the window with zoomed-in pane will be marked with '*' symbol after its name, which is pretty useful to not forget about hidden panes.

That's it. In the next article I will explain how to automate creation of the
session layout which is pretty useful if you build some workflows and do not
want to create the layout manually for every new session. Stay tuned.

