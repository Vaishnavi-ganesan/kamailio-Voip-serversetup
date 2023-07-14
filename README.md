### kamailio-Voip-serversetup
**Step1**: Install mariadb database server
```
sudo apt update
sudo apt install mariadb-server
```
**Step2:** Add Kamailio apt repository
```
wget -O- http://deb.kamailio.org/kamailiodebkey.gpg | sudo apt-key add -
```
Edit ```/etc/apt/sources.list```file depending on the Kamailio version of your choice.
Add the following line at the last of file
```
deb     http://deb.kamailio.org/kamailio57 jammy main
deb-src http://deb.kamailio.org/kamailio57 jammy main
```
The list of APT repositories and associated operating systems is available at http://deb.kamailio.org  

**Step3:** Install Kamailio
```
sudo apt update
sudo apt install kamailio kamailio-mysql-modules
```
To be able to load websocket module, you have to install the package kamailio-websocket-modules:
```
sudo apt install kamailio-websocket-modules kamailio-tls-modules
```
Once the above commands are finished, you can check if ```kamailio``` application is available and confirm installed version using ```kamailio -V```    

**Step 4:** Configure Kamailio 
Edit the file ```/etc/kamailio/kamctlrc``` and make sure the ```DBENGINE``` variable is set to ```MySQL```. Remove the # symbol to uncomment it.
Set Database engine to MYSQL
```
sudo nano /etc/kamailio/kamctlrc
DBENGINE=MYSQL
DBHOST=localhost
```
Next is to create database for Mysql. Command below will create users and tables need by Kamailio(Schema)
```
sudo kamdbctl create
```
You will be prompted to provide a mysql root password. Mysql users and password added by above command are.
kamailio with the password **kamailiorw**. It has read/write access permissions to the Kamailio database.
kamailioro: The password for this user is **kamailioro**. It has read only access permissions to the Kamailio database.
Then,edit
```
sudo nano/etc/kamailio/kamctlrc
```
change sip_domain to your local network by using ```ifconfing```
```
SIP_DOMAIN=192.168.241.120
```
Then add the following in nano /etc/kamailio/kamailio.cfg just below #!KAMAILIO.
```
sudo nano /etc/kamailio/kamailio.cfg
#!define WITH_MYSQL
#!define WITH_AUTH
#!define WITH_USRLOCDB
#!define WITH_ACCDB
```
These directives will turn on necessary modules.  E.g when you specify,WITH_MYSQL it enables the loading of mysql.   

**Step5:** Restart kamailio service
```
sudo systemctl restart kamailio
```
To check the status
```
 systemctl status kamailio
```
If you encounter any issues with Kamailio service, the logs are available on``/var/log/kamailio.log```     

**Step6:** Adding subscriber
Adding Subscribers To add subscribers (users), you can use the kamctl command:
```
kamctl add userid password
```
Like
```
kamctl add 234 234
```
To check the subscriber is added, following command is used
```
kamctl db show subscriber
```
**Step7:** Connection to linphone(androd client) to make a call
Linphone android client was installed in two android phone(Note:Both must be connected to same wifi)
The username,password and sip domain was configured.
And the call is made via linphone



