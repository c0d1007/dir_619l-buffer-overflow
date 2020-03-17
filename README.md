# dir_619l-buffer-overflow

the webserver boa in dlink-619L firmware 2.06beta have a  stack overflow vulnerability

When the router login interface enables graphical verification, the third parameter of the sprintf function in the request /goform/Login, getAuthCode function is the FILECODE parameter, which will copy the parameter to the local variable of the current function, causing a stack overflow and remote code execution.


