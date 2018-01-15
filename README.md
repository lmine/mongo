# mongo


# Prepare machine
```
sudo -s
apt-get update
apt-get dist-upgrade
```
# Install Docker
```
sudo apt-get install \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common
     
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -

apt-key fingerprint 0EBFCD88

add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable"
   
apt-get update
 
apt-get install docker-ce
 
gpasswd -a $USER docker
```

# Add data disk
```
fdisk /dev/sdb
  n
  p
  
mkfs.ext4 /dev/sdb1

UUID=`blkid /dev/sdb1 | awk -F '"' '{print $2}'`
echo "UUID=$UUID /data ext4 defaults 0 1" >> /etc/fstab

```
