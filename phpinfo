# UCMS
## Vulnerability Name:SQL Injection
UCMS has SQL Injection in the installing file.
## Vulnerability version number:
UCMS v1.4.6
## Vulnerability:
high risk
## Location
The vulnerability located in the /install/index.php.
![imgage](https://github.com/blackstar24/UCMS/blob/master/2.png)
![imgage](https://github.com/blackstar24/UCMS/blob/master/1.png) 
## Vulnerability Description:
When in the progress of installing.The database name control is not strict during installation, which can lead to stack query injection.
## payload
aa`;select if(left((select current_user),4)='root',sleep(3),3);`
![imgage](https://github.com/blackstar24/UCMS/blob/master/3.png) 
## Suggestions for rectification:
Filter user input data.
