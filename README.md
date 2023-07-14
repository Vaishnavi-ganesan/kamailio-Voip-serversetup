### kamailio-Voip-serversetup
Step1: Install mariadb database server
```
sudo apt update
sudo apt install mariadb-server
```
Step2: Add Kamailio apt repository
```
wget -O- http://deb.kamailio.org/kamailiodebkey.gpg | sudo apt-key add -
```
Edit ```/etc/apt/sources.list```file depending on the Kamailio version of your choice.
Step3: Install Kamailio
```
sudo apt update
sudo apt install kamailio kamailio-mysql-modules
```
To be able to load websocket module, you have to install the package kamailio-websocket-modules:
```
sudo apt install kamailio-websocket-modules kamailio-tls-modules
```
Once the above commands are finished, you can check if ```kamailio``` application is available and confirm installed version using ```kamailio -V```
