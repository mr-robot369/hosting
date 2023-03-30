
# Get started hosting your personal website 

This repository gives you the code you'll need to know to host your website.
We will use [puTTy](https://www.putty.org/), [FileZilla](https://filezilla-project.org/), and [Apache](https://httpd.apache.org/docs/)

## Documentation

[Documentation](https://1drv.ms/w/s!AqhFoBZNVhLmpSGRRscttYDVF1Wb)


## Contents

- [Initialisation](#--initialisation)

- [File Transfer](#--file-transfer-using-filezilla) ([FileZilla](https://filezilla-project.org/))

- [Server Creation](#--server-creation)

- [Domain Creation](#--domain-creation-using-cloudflare) ([Cloudflare](https://dash.cloudflare.com/3fbf28bc9ec4ec7e68b20cf20daf9f37))

- [Established connection between Server and Client](#--established-connection-between-server-and-client-using-apache2) ([Apache2](https://httpd.apache.org/docs/))


## -> Initialisation

1. Firstly login using your username and password in puTTy. 

2. Then create a parent folder using command mkdir and inside it again create a folder (which contains our proect)

```
mkdir <parent-folder>
cd <parent-folder>
mkdir <folder>
```

![image1](https://user-images.githubusercontent.com/97546428/228840250-a7a6ed17-d3b3-4685-9811-0104c76c00b6.png)

## -> File Transfer (Using FileZilla)

3. Open filezilla and transfer all the files except node_modules folder of your project inside the parikalan folder which we create in above step.

![image2](https://user-images.githubusercontent.com/97546428/228845556-da702193-7ca8-494d-b1d3-578482a17e0d.png)

## -> Server Creation

4. Inside the folder parikalan in puTTy, type command npm install to download the node module in your folder.

```
npm install
```

5. Type a command to start the server
```
pm2 start <js-file> --name <name>
```
where js-file is our  javascript file which link our frontend part with the backend and name is the name visible when we type pm2 status command

- In our case
    ```
    pm2 start index.js --name parikalanexp
    ```
![image3](https://user-images.githubusercontent.com/97546428/228848060-30dbf01f-06fa-41eb-abf7-e9441d24e478.png)
Here we can see parikalanexp is now online.

## -> Domain Creation (Using Cloudflare)

6. Open cloudflare in your browser and login with your email id and password.

![image4](https://user-images.githubusercontent.com/97546428/228850405-565e2ba9-3e09-4989-b03b-6aa30c55eadc.png)

7. Click on pgdavhyperion.in and then click on DNS -> records

![image5](https://user-images.githubusercontent.com/97546428/228850687-e0b877aa-6317-4139-9750-afa589e8e0d3.png)

8. Click on Add Records and fill CNAME in “type” and in “Name” type the site name (eg. parikalantest) and in “IPv4 address” type pgdavhyperion.in and then click on Save.
![image6](https://user-images.githubusercontent.com/97546428/228850755-2c03a285-ad75-45dd-bf91-ce467eb5bb8e.png)

## -> Established connection between Server and Client (Using Apache2)

9. In puTTy, we have to type a command to enter in sites-available directory inside apache folder and then create a file with .conf extension

```
cd /etc/apache2/
cd sites-available 
nano <file-name>.conf
```
 - In our case,
    ```
    nano parikalantest.conf
    ```

- 'sites-available' directory contains file with extension '.conf' which contains all the information needed to host the site such as port, domain name etc.

10. Inside parikalantest.conf type the following commands: 
```
<VirtualHost *:80>
    ServerName <site name>.<domain name>
 
    ProxyPreserveHost On
    ProxyPass / http://localhost:<port>/
    ProxyPassReverse / http://localhost: <port>/
</VirtualHost>

```
- press 'CTRL+X and theb enter' to save the file

![image8](https://user-images.githubusercontent.com/97546428/228850905-6c7e548e-a726-458d-827b-ead366982c1f.png)

11. Then type following commands:
```
a2ensite <conf filename>
systemctl reload apache2
```
![image9](https://user-images.githubusercontent.com/97546428/228850961-2c68b606-c594-42da-9db0-11b753c358fb.png)
