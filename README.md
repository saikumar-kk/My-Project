FitInfinite App
===============


Introduction
------------

FitInfinite is an on-demand sports and fitness marketplace for Professionals and Amateurs 


Environment Details
-------------------

### Supported Operating Systems

Linux (Ubuntu-1x.xx)

### System Requirements
Intel processor, 2GB RAM, 50GB HDD free Space.

### Prerequisites
The FitInfinite Admin portal has the following prerequisites. The following packages needs to be installed in the machine where we launch the FitInfinite AP web Application.

### Software Requirements

#### Application

1. Nodejs 5.10.1
2. Postgresql 9.5
3. Virtualbox 5.x.x
4. Vagrant 1.8.x 
5. Ansible 2.x.x.x


#### Application packages installed in vagrant VM's
1. Nodejs 5.10.1
2. Postgres 9.5.x

#### JAVA Script additional packages installed in vagrant (should be in dependency section of package.json)
1. express 4.13.4
2. epress-session 1.13.0
3. passport 0.3.2
4. passport-local 1.0.0
5. pg 4.5.3
6. sequelize 3.21.0
7. sequelize-fixtures 0.5.1
8. uuid 2.0.2
9. bcrypt 0.8.5
10. body-parser 1.15.0
11. morgon 1.7.0
12. raml2html 2.4.0


Steps to launch FitInfinite APP
===============================

System Prep
-----------

1. Install software as root

```
$ sudo apt-get update
$ sudo apt-get install virtualbox 
$ sudo apt-get install vagrant
```


2. As root, create a Base Box using vagrant
```
$ vagrant box add fitinfinite-dev /path/to/the/new.box
[...]
$ vagrant init fitinfinite-dev
[...]
$ vagrant up
```

3. Install Software in newly created VM box by using ansible (vagrant provision)
   (Update vagrant configuration file to ansible setup provision)
```
$ vagrant provision
[...]
```

App Setup
---------


1. As root, create a folder for your fitinfinite_app.  I chose `/vagrant/fitinfinite-app`.
```
$ mkdir -p /vagrant/fitinfinite_app
$cd /vagrant/fitinfinite_app
```


2. Install dependency java script libraries by using package manager (should be in package.json)
```
$ npm install 

```

3. Checkout the source
```
$ cd /vagrant/fitinfinite_app
$ git init
$ git remote add origin https://github.com/fitinfinite/fitinfinite-mobax-backend.git
$ git fetch --all
$ git checkout v0.1.0-albha.100
```

Database Setup
--------------


4. Set up the database as root/postgres
```
$ sudo -u postgres psql
postgres=# create database fitinfinite;
postgres=# create role fitadmin with login password 'fitadmin';
postgres=# grant all on database fitinfinite to fitadmin;
postgres=# \q
$ exit
```
5. Content updated


