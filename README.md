# Zabbix-GNS3-AWS
This lab helps you to build GNS3 lab on a remote server at the AWS add Zabbix and start monitor network elements from the GNS3 topology.

![Zabbix-GNS3 diagram](Zabbix-Zabbix-Lab.drawio.png)

# GNS3 remote AWS server

## Install Remote GNS3 server



1) Firstly you would need to run EC2 instance. We will skip this part as you may use your own options, but for simplicity just choose
   + Recent Ubunutu image
   + t2.large or t2.xlarge should be enough
   + RAM 8GB+
   + Better to have something more then 16GB (32 or 64+) of storage
   + Highly recommended to add Elastic IP so you have you GNS3 always availble with the same IP even after restarts
   + Do not forget to update Secure_groups with OpenVPN protocols
      - UDP 1194
      - TCP 8003
      - TCP 3080
      -  Some other ports like SSH(22), HTTP/HTTPS (80/443)
          
2) Those commands will allow you to install GNS3 and run the script to configure it with OpenVPN to secure your client-to-server connection

   ```
   cd /tmp
   ```
   Downlowd install script from GNS3 git
   ```
   curl https://raw.githubusercontent.com/GNS3/gns3-server/master/scripts/remote-install.sh > gns3-remote-install.sh
   ```
   Run the script
   ```
   bash gns3-remote-install.sh --with-openvpn --with-iou --with-i386-repository
   ```
   > [!NOTE]
   > Those command may require ```sudo``` to be used

3) Now script will run everything you need. Once done: 
    Reboot
    ```
    sudo reboot now
    ```
    After reboot on a welcome screen you will find URL to grab your OpenVPN config file
    Now open your OpenVPN client and add config file
    Now you can connect. Be sure that your VPN is now active and you see "Connected"

## Configure GNS3 client

1) Your GNS3 client (assuming you have installed it already from the  [**official web site**](https://www.gns3.com/))
2) Now let's configure GNS3 client to connect to the AWS server
   + Go to the GNS3-->Preferences-->Server-->Be sure that "Enable local server" checkbox is unchecked
   + In the Host field just type your VPN IP address. You can find it on a welcome screen after OpenVPN installation. Usually it is 172.16.253.1
   + You can leave all other fields untouched 
