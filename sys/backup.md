# Exemple making a remote backup

````
sshfs -p13143 appbox@vnc.37rtm.appboxes.co:/APPBOX_DATA/storage /mnt/remote1/ -o allow_other
borg list /mnt/remote1/borg::vps01 mnt/sdb1/home/nheim/src
````
