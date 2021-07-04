# MongoDB-ARM64
MongoDB binaries build on (and for) Raspberry Pi 4B 4GB.

Includes **Mongo Database Tools** (mongodump, mongosretore, mongoimport...),
and configuration files for Raspberry Pi OS 64-bit.

## Installation

1. Download the zip archive and copy (sudo cp -r) *etc*, *lib*, *usr* folders contents into your local *etc*, *lib*, *usr* folders.

2. Create mongodb user.

`sudo useradd -M mongodb`

`sudo groupadd mongodb`

`sudo su`

`/usr/sbin/usermod -L mongodb`

`/usr/sbin/usermod -a -G mongodb mongodb`

`exit`

`grep mongodb /etc/group`

3. Create required directories & make them own by previously created "mongodb" user.

`sudo mkdir -p /var/lib/mongodb`

`sudo mkdir -p /var/log/mongodb`

`sudo chown mongodb:mongodb /var/lib/mongodb`

`sudo chown mongodb:mongodb /var/log/mongodb`

4. Settings to start MongoDB server at system startup, launch mongo and check the status.

`sudo systemctl daemon-reload`

`sudo systemctl enable mongod`

`sudo systemctl start mongod`

`sudo systemctl status mongod`

5. Finish.

Now restart your system `sudo reboot now`, once back enter into MongoShell `mongo`.

If you see MongoDB server's version then try to create an admin user for the database.

`use admin`

`db.createUser( { user: "admin",
            pwd: "SUPERSECRETPASSWORD",
            roles: [ "userAdminAnyDatabase",
                     "dbAdminAnyDatabase",
                     "readWriteAnyDatabase"] } )`
                     
`exit`

Inspired from [HOWTO: Install MongoDB 4.4.3 on RPi OS 64bit](https://www.raspberrypi.org/forums/viewtopic.php?t=300028)
