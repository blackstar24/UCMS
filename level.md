# UCMS
## Vulnerability Name:Level override
UCMS has Level override in the user/editpost.php.
## Vulnerability version number:
UCMS v1.4.6
## Vulnerability:
high risk
## Location
The vulnerability located in the user/editpost.php.
## Vulnerability Description:
1.First the program check the user's level and then give the superuser level 3,administor level 2,and normal user level 1,
Then if the user is not belong to the group of superuser,their level will be subtracted.

![imgage](https://github.com/blackstar24/UCMS/blob/master/15.png) 

2.Line 86 has a geadminname() function, which is used to get the current user identity from the cookie. Let's follow it here.
The function definition is obtained on line 55 of ucms/chk.php. The cookie's key is stitched with a constant cookiehash using the string ‘admin_’. 
Line 66 has a setadminname() function that defines the cookie. Then let's take a look at the definition of this constant.
![imgage](https://github.com/blackstar24/UCMS/blob/master/16.png) 
![imgage](https://github.com/blackstar24/UCMS/blob/master/17.png) 

3.The constant declared in the /ucms/admin_config.php file, followed by the constant Sitehash
![imgage](https://github.com/blackstar24/UCMS/blob/master/18.png)
4.Inside inc/config.php, it is a random seed. So here we know that the name of the cookie is formed by the 'admin_' splicing random seed in the first 6 characters after the md5 digest.

![imgage](https://github.com/blackstar24/UCMS/blob/master/19.png) 

5.Then we look at the value of the setadminname() function. In the login.php file, 55 lines call this function to set the value of the cookie. 
The parameters of the second function are derived from the user name queried by the database. The username in the original sql statement comes from the user name of the post submitted by the login page $_POST ['uuu_username'].
![imgage](https://github.com/blackstar24/UCMS/blob/master/20.png) 

6.Then look at the reason, $username comes from the results of the $id and $alevel queries, that is, the database records, 
the condition to be met is that there must be a superadmin in the system, the username permission to be changed is not less than the value specified by alevel.
![imgage](https://github.com/blackstar24/UCMS/blob/master/21.png) 
## payload
Log in to the background, click on the account management to modify the current user sadmin,
fill in the password 123456 and submit the package.
![imgage](https://github.com/blackstar24/UCMS/blob/master/22.png) 
![imgage](https://github.com/blackstar24/UCMS/blob/master/23.png) 

Here, the id=3 in the parameter is changed to id=1 (the built-in admin account is installed when the system is installed, the id is 1), 
and then the code below is updated by the id with the user name admin.

$query = $GLOBALS['db'] -> query("UPDATE ".tableex('admin')." SET nickname='$nickname',alevel='".$quan['alevel']."',power='$thispower'$sql WHERE id='$id'");

After the modification is successful, log in to the system with admin and 123456.
## Suggestions for rectification:
strict the user's level and check the level before the modification.
