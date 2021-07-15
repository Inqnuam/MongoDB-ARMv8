# MongoDB-ARM64
MongoDB for Raspberry Pi OS 64-bit.

Includes **Mongo Database Tools** (mongodump, mongosretore, mongoimport...),
and configuration files for Raspberry Pi OS 64-bit.

## Installation
1. Download Release archive and unzip.

`cd ~ && wget -q -O MongoARM64.zip https://github.com/Inqnuam/MongoDB-ARMv8/releases/download/v5.0.0/MongoDBv5.0.0_ARM64.zip && unzip MongoARM64.zip && rm MongoARM64.zip`

2. Stop MongoDB Server if a previous version is running.

`sudo systemctl stop mongod`

3. Copy all binaries and required files into **/**.

`sudo cp -r MongoARM64/install/* /`

4. Finish. You can now reboot your Raspberry Pi.

Next steps are required if this is your first MongoDB installation on your Pi.

## Fresh new installation

5. Create mongodb user.

`sudo useradd -M mongodb`

`sudo groupadd mongodb`

`sudo su`

`/usr/sbin/usermod -L mongodb`

`/usr/sbin/usermod -a -G mongodb mongodb`

`exit`

`grep mongodb /etc/group`

6. Create required directories & make them own by previously created "mongodb" user.

`sudo mkdir -p /var/lib/mongodb`

`sudo mkdir -p /var/log/mongodb`

`sudo chown mongodb:mongodb /var/lib/mongodb`

`sudo chown mongodb:mongodb /var/log/mongodb`

7. Settings to start MongoDB server at system startup, launch mongo and check the status.

`sudo systemctl daemon-reload`

`sudo systemctl enable mongod`

`sudo systemctl start mongod`

`sudo systemctl status mongod`

8. Finish.

Now restart your system `sudo reboot now`, once back enter into MongoShell `mongo` or into brand new `mongosh` which is recommanded.

If you see MongoDB server's version then try to create an admin user for the database.

`use admin`

`db.createUser( { user: "admin",
            pwd: "SUPERSECRETPASSWORD",
            roles: [ "userAdminAnyDatabase",
                     "dbAdminAnyDatabase",
                     "readWriteAnyDatabase"] } )`
                     
`exit`

Remove installation files

`cd ~ && rm -rf MongoARM64`

Inspired from [HOWTO: Install MongoDB 4.4.3 on RPi OS 64bit](https://www.raspberrypi.org/forums/viewtopic.php?t=300028)
