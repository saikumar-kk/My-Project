FitInfinite Solution
===============


Introduction
---------------

FitInfinite is an on-demand sports and fitness marketplace for Professionals and Amateurs. Refer the Prdocuct Requirements document or the Software Requirements Specification for more the functionality of the solution. 


Environment Details
--------------------------

### Supported Operating Systems

Linux (Ubuntu-1x.xx)

### System Requirements
Intel processor (<min config here> or equivalent)
2GB RAM, 
50GB HDD free Space.

### Prerequisites
The FitInfinite Admin portal has the following prerequisites. The following packages need to be installed where we host the FitInfinite solution.

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
7. sequelize-cli 2.4.0
8. uuid 2.0.2
9. bcrypt 0.8.5
10. body-parser 1.15.0
11. morgon 1.7.0
12. genpasswd 0.1.3
13. hashids 1.0.2
14. connect-flash 0.1.1
15. ejs 2.4.1
16. nodemailer 0.7.1


Steps to set up the FitInfinite solution
========================

Environment Setup 
------------------------

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

3. Install Software in the newly created VM box by using ansible (vagrant provisioner)
   (Update vagrant configuration file for ansible setup and provisioning)
```
$ vagrant provisioning
[...]
```



Solution Setup
------------------


1. Connect vagrant vm's by using 'vagrant ssh'
2. Create a folder for your fitinfinite_app.  I chose `/vagrant/fitinfinite-app`.
```
$ mkdir -p /vagrant/fitinfinite_app
$cd /vagrant/fitinfinite_app
```


3. Install dependency java script libraries by using package manager (should be in package.json)

```
$ npm install 

```

4. Checkout the source

```
$ cd /vagrant/fitinfinite_app
$ git init
$ git remote add origin https://github.com/fitinfinite/fitinfinite-mobax-backend.git
$ git fetch --all
$ git checkout v0.1.0-albha.100
```

Database Setup
-------------------


4. Set up the database as root/postgres
```
$ sudo -u postgres psql
postgres=# create database fitinfinite;
postgres=# create role fitadmin with login password 'fitadmin';
postgres=# grant all on database fitinfinite to fitadmin;
postgres=# \q
$ exit
```

5. Initial data setup [ DB migration using sequelize-cli tool] as follows
```
$ cd app/
$ ../node_modules/sequelize-cli/bin/sequelize db:migrate
[...]
$ ../node_modules/sequelize-cli/bin/sequelize db:seed:all
[...] 
```
6. Server startup
```
$ node server.js
[...] 
```

Unit Test
---------------

We are using Mocha and Chai for unit test cases


How to install Mocha and Chai?
--------------------------------

It's easy to install Mocha and Chai with the following commands:

```
$ npm install mocha --save-dev
$ npm install chai --save-dev
$ npm install supertest --save-dev
```

Structure
---------------

To set up the tests, create a new folder called “test” in the project root, then within that folder divide into admin and clientapp. Admin console unit tests will handle in admin and mobile client unit tests will handle in clientapp.

    ├── app                   
    ├── config                    
    ├── raml                     
    ├── test                    
        ├── admin                   
        ├── clientapp

Steps for run mocha
--------------------------------

1. Go to project root
```
$ cd /vagrant/fitinfinite_app/
```

2. Run all test cases and extract results to file
```
$ mocha --recursive > fit_unit_test.txt
```

3. View results
```
$ vim fit_unit_test.txt
```

