![st-enchanted](https://user-images.githubusercontent.com/39852038/110760690-03f82f00-8260-11eb-94e0-1aa5886c3cee.png)

st-enchanted - simple terminal enchanted
--------------------
st-enchanted is a customized version of st that designed for tmux and vim


Requirements
------------
In order to build st-enchanted you need the Xlib header files.


Patches
------------
- alpha
- boxdraw
- harfbuzz
    

Installation
------------
Enter the following command to build and install st-enchanted:

    make clean install


Customization
------------
In order to make your own configurations, edit the ~/.Stdefaults file and then enter the following command (reboot st after the command):

    xrdb -merge ~/.Stdefaults


Uninstallation
------------
Enter the following command to uninstall st-enchanted completely from the machine:

    make clean uninstall
