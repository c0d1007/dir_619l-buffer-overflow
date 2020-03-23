# dir_619l-buffer-overflow

Vender ：D-Link

Firmware version:2.06beta

Exploit Author: ys110

Vendor Homepage: http://www.dlink.com.cn/

Hardware Link:http://support.dlink.com.cn/ProductInfo.aspx?m=DIR-619L

##Vul detail

the webserver boa in dlink-619L firmware 2.06beta have a  stack overflow vulnerability

![image](https://github.com/hhhhu8045759/dir_619l-buffer-overflow/blob/master/619_2.png)

When the router login interface enables graphical verification, the third parameter of the sprintf function in the request /goform/Login, getAuthCode function is the FILECODE parameter, which will copy the parameter to the local variable of the current function, causing a stack overflow and remote code execution.

An attacker can specially construct an http request containing filecode parameters to cause an overflow


