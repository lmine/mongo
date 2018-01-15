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

apt-get install xfsprogs

fdisk /dev/sdb
  n
  p
  
mkfs.xfs /dev/sdb1

UUID=`blkid /dev/sdb1 | awk -F '"' '{print $2}'`
echo "UUID=$UUID /data xfs defaults 0 1" >> /etc/fstab

```

# Init mongodb

```
docker run -it --name mongo1 -d -v /data/db:/data/db mongo --auth
docker exec -it mongo1 mongo admin
     > db.createUser({user:"admin",pwd:"$PASSWORD", roles:[{role:"root",db:"admin"}]})
     > use test
     > db.createUser({user: "mongouser", pwd: "someothersecret", roles: ["readWrite"]})
     > exit
     
eg:
docker exec -it mongo1 mongo mongo -u mongouser -p "someothersecret" --authenticationDatabase test
```
