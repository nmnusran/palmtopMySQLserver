Creating a low-cost palmtop MySQL database server
================================================

**Naufer Nusran.  Feb 4, 2023**

In this project, you will install a server (lite) version of a suitable linux distribution on a palmtop mini computer such as a Raspberry Pi. In your regular PC (the laptop or desktop), you may install MySQL Workbench community version. After creating the database server on your palmtop and also configuring MySQL Workbench on your PC properly, you will be able to remotely access the database server.

Although either a Raspberry Pi 3 or 4 can be used, I would recommend a Raspberry Pi 4, because it is 64bit in contrast to the Raspberry Pi 3 which is 32bit. 

Here, I shall focus on how to make this work on a Libre Computer Board AML-S905X-CC (Le Potato) 2GB 64-bit Mini Computer. The Libre computer is based on ARMv8 Cortex-A53 64bit processor, and is quite comparable to Raspberry Pi 4 specs, for a much lower cost. At the time of preparing this document, you can purchase this in Amazon for only $35.

We also need a micro SD card. I used a SanDisc 128GB card.

Installing the OS for Raspberry Pi:
----------------------------------

First you need to install a suitable OS on the SD card to be used in your palmtop. Download the Raspberry Pi Imager on to your PC (laptop or desktop) that has an SD card reader. 

If your palmtop is a Raspberry Pi 4, install the Raspberry Pi OS Lite (64-bit) version. (Install the 32bit Lite version if it is a Raspberry Pi 3)

Note that “OS Lite” version will not have a desktop GUI. We don’t need a GUI for the OS, because we are creating a server and we will eventually connect to the server remotely.

Installing the OS for Libre Computer:
------------------------------------

Download a suitable OS image of a Ubuntu server for the Libre board from:
https://distro.libre.computer/ci/ubuntu/22.04/

What I have got is a Libre AML-S905X-CC. Therefore, I chose the OS image named “ubuntu-22.04.1-preinstalled-server-arm64+aml-s905x-cc.img.xz”. Note that “server" version will not have a desktop GUI unlike a “desktop” version of Ubuntu.

Once image is downloaded, you can use the same Raspberry Pi Imager utility to install the downloaded image onto your SD Card. 

Installing the Database Server:
------------------------------

Once you switch ON the palmtop with the loaded SD card that already has the OS installed, you may now start installing the database server. Let’s first update the packages using the following Linux terminal command:

sudo apt update && sudo apt upgrade

We will be installing MariaDB server which is essentially based on MySQL.

**sudo apt install mariadb-server**

Then make the necessary database server configurations by typing the following command in the terminal.

**sudo mysql_secure_installation**

You can use the following command to locally connect to the database server with “root” privileges:

**sudo mysql -u root -p**

Congratulations!!!. You have now created and entered the database server!
You may now create or import databases, create database users, grant different privilege levels to different users etc. Getting yourself familiar with SQL commands can be very handy at this point.

Here’re some “administrative” commands I often use:

**CREATE DATABASE yourDB;**

**SHOW DATABASES;**

**CREATE USER 'user1'@'localhost' IDENTIFIED BY 'password1';**

**GRANT ALL PRIVILEGES ON *.* TO ‘user1’@'localhost' IDENTIFIED BY 'password1';**

**FLUSH PRIVILEGES;**

**SHOW GRANTS FOR 'user1'@'localhost';**

**DROP USER 'user1'@'localhost';**

**DROP DATABASE yourDB;**


Setting up MySQL Workbench on your PC:
-------------------------------------

Download the MySQL Workbench free version to your PC (laptop or desktop) from:

https://dev.mysql.com/downloads/workbench/

MySQL Workbench is a user-friendly GUI. After installation, you will have to configure its setting so that it can connect to the database server located in the remote palmtop via SSH. Here’re the settings for MySQL Workbench:

**Connection method => standard TCP/IP over SSH**

**SSH Hostname => palmtop IP : ssh port**

**SSH Username => ssh username**

**MYSQL Hostname => localhost or 127.0.0.1**

**MYSQL Server port => 3306**




![Libre](https://user-images.githubusercontent.com/48889316/217903637-d68181e2-f43d-4b94-80e7-89cf4ec31b79.png)
