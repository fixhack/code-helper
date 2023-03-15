## dnsmasq installation & configuration

install dnsmasq

    sudo apt install dnsmasq
    sudo systemctl restart dnsmasq

    sudo nano /etc/resolv.conf 
    sudo nano /etc/dnsmasq.conf
    sudo mkdir /etc/hosts.d 
    sudo nano /etc/dnsmasq.d/teqsoft-home_xyz.conf
    sudo mv /etc/dnsmasq.d/teqsoft-home_xyz.conf /etc/dnsmasq.d/teqsoft_xyz.conf 
    sudo mv /etc/hosts.d/hosts_teqsoft-home_xyz /etc/hosts.d/hosts_teqsoft_xyz 

## samba

install samba

    udisksctl mount -b /dev/sda1

    sudo apt install samba
    sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bkp
    sudo mkdir /media/ubuntu
    sudo cp ./smb.conf /etc/samba/smb.conf
    sudo systemctl restart smbd
    sudo systemctl restart nmbd
    sudo systemctl status smbd
    sudo smbpasswd -a ubuntu
    sudo smbpasswd -e ubuntu
    sudo chown ubuntu:ubuntu /media/ubuntu
    sudo chmod g+rw /media/ubuntu

## p7zip

install p7zip

    sudo apt install p7zip

## podman

install podman

    sudo apt install podman
    
