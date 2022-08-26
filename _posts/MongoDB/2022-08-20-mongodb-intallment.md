---
layout: single

title:  "MongoDB Installment"
excerpt: ""

categories: 
    - MongoDB
tags: [nosql, mongodb]

toc: true
author_profile: false
sidebar:
    nav: "docs"

date: 2022-08-20
last_modified_at: 2022-08-20
---

#### 1. Import the public key used by the package management system.
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -

#### 2. Create a list file for MongoDB.
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list

#### 3. Reload local package database.
sudo apt-get update

#### 4. Install the MongoDB packages.
sudo apt-get install -y mongodb-org

--

#### 1. Start MongoDB.
sudo systemctl daemon-reload
sudo systemctl start mongod

#### 2. Verify that MongoDB has started successfully.
sudo systemctl status mongod

sudo systemctl enable mongod

#### 3. Stop MongoDB.
sudo systemctl stop mongod

#### 4. Restart MongoDB
sudo systemctl restart mongod

#### 5. Begin using MongoDB
You can run mongosh without any command-line options 
to connect to a mongod that is running on your localhost with default port 27017.

mongosh

---

#### Uninstall MongoDB

sudo service mongod stop
sudo apt-get purge mongodb-org*
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb

---

![image1](/assets/images/mongodb/mongodb-gpg-key.png)
![image2](/assets/images/mongodb/systemctl-mongodb.png)
![image3](/assets/images/mongodb/mongosh.png)