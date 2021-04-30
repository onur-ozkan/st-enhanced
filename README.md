st-enhanced - simple terminal enhanced
--------------------
st-enhanced is a customized version of st that makes using tmux and vim much better


Requirements
------------
In order to build st-enhanced you need the Xlib header files.


Installation
------------
Enter the following command to build and install st-enhanced:

    sudo make clean install


Customization
------------
In order to make your own configurations, copy .Stdefaults anywhere you want, and then edit the ~/.Stdefaults file and then enter the following command (reboot st after the command):

    xrdb -merge .Stdefaults

Shortcuts
------------
| command								    | role						                |
| -											| -										    |
| **alt + s**								| increase transparency			            |
| **alt + a**								| decrease transparency		                |
| **alt + shift + up-arrow**				| zoom in									|
| **alt + shift + down-arrow**				| zoom out					                |
| **alt + c**								| copy selected text			            |
| **alt + v**								| paste copied text			                |


Shortcuts
------------
Besides the default shortcuts, you will have the followings also:
- `alt + a` = **decrease transparency**
- `alt + shift + up-arrow` = **zoom in**
- `alt + shift + down-arrow` = **zoom out**
- `alt + c` = **copy selected text**
- `alt + v` = **paste copied text**


Uninstallation
------------
Enter the following command to uninstall st-enhanced completely from the machine:

    sudo make clean uninstall
