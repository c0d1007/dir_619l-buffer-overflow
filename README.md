# dir_619l-buffer-overflow

The router is set to open the graphical login. An unauthorized attacker can send attack packets to cause code execution.

When the router login interface enables graphical verification, the third parameter of the sprintf function in the request /goform/Login, getAuthCode function is the FILECODE parameter, which will copy the parameter to the local variable of the current function, causing a stack overflow and remote code execution.
