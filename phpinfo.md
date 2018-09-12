# UCMS
## Vulnerability Name:
An issue was discovered in UCMS. It allows PHP code injection via the systemdomain parameter to install/index.php, as demonstrated by injecting a phpinfo() call into /inc/config.php.
## Vulnerability version number:
UCMS v1.4.6
## Vulnerability:
high risk
## Location
The vulnerability located in the /install/index.php.
![imgage](https://github.com/blackstar24/UCMS/blob/master/4.png)
![imgage](https://github.com/blackstar24/UCMS/blob/master/5.png) 
![imgage](https://github.com/blackstar24/UCMS/blob/master/6.png) 
## Vulnerability Description:
When in the progress of installing.The systemdomain name control is not strict during installation, which can lead to PHP code executed.
## Payload
1');phpinfo();#

![imgage](https://github.com/blackstar24/UCMS/blob/master/7.png) 
![imgage](https://github.com/blackstar24/UCMS/blob/master/8.png) 
![imgage](https://github.com/blackstar24/UCMS/blob/master/9.png)
## Suggestions for rectification:
Filter user input data.
