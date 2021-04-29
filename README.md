st-enchanted - simple terminal enchanted
--------------------
st-enchanted is a customized version of st that makes using tmux and vim much better


Requirements
------------
In order to build st-enchanted you need the Xlib header files.


Installation
------------
Enter the following command to build and install st-enchanted:

    sudo make clean install


Customization
------------
In order to make your own configurations, copy .Stdefaults anywhere you want, and then edit the ~/.Stdefaults file and then enter the following command (reboot st after the command):

    xrdb -merge .Stdefaults

Shortcuts
------------
Besides the default shortcuts, you will have the followings also:
- `alt + s` = **increase transparency**
- `alt + a` = **decrease transparency**
- `alt + shift + up-arrow` = **zoom in**
- `alt + shift + down-arrow` = **zoom out**
- `alt + c` = **copy selected text**
- `alt + v` = **paste copied text**


Uninstallation
------------
Enter the following command to uninstall st-enchanted completely from the machine:

    sudo make clean uninstall
