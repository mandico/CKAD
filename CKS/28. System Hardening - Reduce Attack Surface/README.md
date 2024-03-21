Host OS Footprint

IAM Roles

Network Access

apt-get update && apt-get install vsftpd samba
systemctl start vsftpd
systemctl start smbd
ps -aux 
netstat -plnt | grep smbd
netstat -plnt | grep vsftpd

### Find and disabled the application that is listerner on port 21

netstat -plnt | grep 21
lsoft -i :21
systemctl list-units --type service | grep ftp
systemctl status sftpd
systemctl stop sftpd
systemctl disable sftpd
netstat -plnt | grep 21
lsoft -i :21

### Investigate Linux Users

whoami
cat /etc/passwd
