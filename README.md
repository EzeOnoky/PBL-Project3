# PBL-Project3
Darey.io DevOps Project Based Learning PBL3

In this project, i will implement a web solution based on MERN stack in AWS Cloud.
MERN Web stack consists of following components:
MongoDB: A document-based, No-SQL database used to store application data in a form of documents.
ExpressJS: A server side Web Application framework for Node.js.
ReactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.
Node.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.

![PBL3_Picture1](https://user-images.githubusercontent.com/122687798/219295295-2f4b71f3-bb5b-4651-aea2-313b81faa2c3.JPG)

As shown on the illustration above, a user interacts with the ReactJS UI components at the application front-end residing in the browser. This frontend is served by the application backend residing in a server, through ExpressJS running on top of NodeJS.

Any interaction that causes a data change request is sent to the NodeJS based Express server, which grabs data from the MongoDB database if required, and returns the data to the frontend of the application, which is then presented to the user.


## STEP 1 – BACKEND CONFIGURATION

ubuntu@ip-172-31-51-131:~$
ubuntu@ip-172-31-51-131:~$
ubuntu@ip-172-31-51-131:~$
ubuntu@ip-172-31-51-131:~$ sudo apt update
Hit:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy InRelease
Get:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]
Get:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports InRelease [107 kB]
Get:4 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]
Get:5 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy/universe amd64 Packages [14.1 MB]
Get:6 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy/universe Translation-en [5652 kB]
Get:7 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy/universe amd64 c-n-f Metadata [286 kB]
Get:8 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy/multiverse amd64 Packages [217 kB]
Get:9 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy/multiverse Translation-en [112 kB]
Get:10 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy/multiverse amd64 c-n-f Metadata [8372 B]
Get:11 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [896 kB]
Get:12 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main Translation-en [196 kB]
Get:13 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 c-n-f Metadata [13.5 kB]
Get:14 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [624 kB]
Get:15 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/restricted Translation-en [96.1 kB]
Get:16 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 c-n-f Metadata [580 B]
Get:17 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 Packages [811 kB]
Get:18 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/universe Translation-en [147 kB]
Get:19 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 c-n-f Metadata [15.5 kB]
Get:20 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 Packages [9696 B]
Get:21 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/multiverse Translation-en [3260 B]
Get:22 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 c-n-f Metadata [456 B]
Get:23 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports/main amd64 Packages [40.7 kB]
Get:24 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports/main Translation-en [9800 B]
Get:25 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports/main amd64 c-n-f Metadata [392 B]
Get:26 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports/restricted amd64 c-n-f Metadata [116 B]
Get:27 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports/universe amd64 Packages [19.5 kB]
Get:28 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports/universe Translation-en [13.8 kB]
Get:29 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports/universe amd64 c-n-f Metadata [392 B]
Get:30 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports/multiverse amd64 c-n-f Metadata [116 B]
Get:31 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [637 kB]
Get:32 http://security.ubuntu.com/ubuntu jammy-security/main Translation-en [133 kB]
Get:33 http://security.ubuntu.com/ubuntu jammy-security/main amd64 c-n-f Metadata [8388 B]
Get:34 http://security.ubuntu.com/ubuntu jammy-security/restricted amd64 Packages [575 kB]
Get:35 http://security.ubuntu.com/ubuntu jammy-security/restricted Translation-en [87.9 kB]
Get:36 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 Packages [640 kB]
Get:37 http://security.ubuntu.com/ubuntu jammy-security/universe Translation-en [88.1 kB]
Get:38 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 c-n-f Metadata [11.3 kB]
Get:39 http://security.ubuntu.com/ubuntu jammy-security/multiverse amd64 Packages [4960 B]
Get:40 http://security.ubuntu.com/ubuntu jammy-security/multiverse Translation-en [996 B]
Get:41 http://security.ubuntu.com/ubuntu jammy-security/multiverse amd64 c-n-f Metadata [240 B]
Fetched 25.8 MB in 4s (5747 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
7 packages can be upgraded. Run 'apt list --upgradable' to see them.
ubuntu@ip-172-31-51-131:~$
ubuntu@ip-172-31-51-131:~$ sudo apt upgrade
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
The following NEW packages will be installed:
  linux-aws-headers-5.15.0-1030 linux-headers-5.15.0-1030-aws linux-image-5.15.0-1030-aws
  linux-modules-5.15.0-1030-aws
The following packages have been kept back:
  ubuntu-advantage-tools
The following packages will be upgraded:
  git git-man less linux-aws linux-headers-aws linux-image-aws
6 upgraded, 4 newly installed, 0 to remove and 1 not upgraded.
6 standard LTS security updates
Need to get 53.4 MB of archives.
After this operation, 231 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 less amd64 590-1ubuntu0.22.04.1 [143 kB]
Get:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 git-man all 1:2.34.1-1ubuntu1.8 [953 kB]
Get:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 git amd64 1:2.34.1-1ubuntu1.8 [3141 kB]Get:4 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-modules-5.15.0-1030-aws amd64 5.15.0-1030.34 [22.5 MB]
Get:5 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-image-5.15.0-1030-aws amd64 5.15.0-1030.34 [11.4 MB]
Get:6 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-aws amd64 5.15.0.1030.28 [1716 B]Get:7 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-image-aws amd64 5.15.0.1030.28 [2458 B]
Get:8 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-aws-headers-5.15.0-1030 all 5.15.0-1030.34 [12.4 MB]
Get:9 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-headers-5.15.0-1030-aws amd64 5.15.0-1030.34 [2822 kB]
Get:10 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates/main amd64 linux-headers-aws amd64 5.15.0.1030.28 [2390 B]
Fetched 53.4 MB in 2s (33.9 MB/s)
(Reading database ... 63605 files and directories currently installed.)
Preparing to unpack .../0-less_590-1ubuntu0.22.04.1_amd64.deb ...
Unpacking less (590-1ubuntu0.22.04.1) over (590-1build1) ...
Preparing to unpack .../1-git-man_1%3a2.34.1-1ubuntu1.8_all.deb ...
Unpacking git-man (1:2.34.1-1ubuntu1.8) over (1:2.34.1-1ubuntu1.6) ...
Preparing to unpack .../2-git_1%3a2.34.1-1ubuntu1.8_amd64.deb ...
Unpacking git (1:2.34.1-1ubuntu1.8) over (1:2.34.1-1ubuntu1.6) ...
Selecting previously unselected package linux-modules-5.15.0-1030-aws.
Preparing to unpack .../3-linux-modules-5.15.0-1030-aws_5.15.0-1030.34_amd64.deb ...
Unpacking linux-modules-5.15.0-1030-aws (5.15.0-1030.34) ...
Selecting previously unselected package linux-image-5.15.0-1030-aws.
Preparing to unpack .../4-linux-image-5.15.0-1030-aws_5.15.0-1030.34_amd64.deb ...
Unpacking linux-image-5.15.0-1030-aws (5.15.0-1030.34) ...
Preparing to unpack .../5-linux-aws_5.15.0.1030.28_amd64.deb ...
Unpacking linux-aws (5.15.0.1030.28) over (5.15.0.1028.26) ...
Preparing to unpack .../6-linux-image-aws_5.15.0.1030.28_amd64.deb ...
Unpacking linux-image-aws (5.15.0.1030.28) over (5.15.0.1028.26) ...
Selecting previously unselected package linux-aws-headers-5.15.0-1030.
Preparing to unpack .../7-linux-aws-headers-5.15.0-1030_5.15.0-1030.34_all.deb ...
Unpacking linux-aws-headers-5.15.0-1030 (5.15.0-1030.34) ...
Selecting previously unselected package linux-headers-5.15.0-1030-aws.
Preparing to unpack .../8-linux-headers-5.15.0-1030-aws_5.15.0-1030.34_amd64.deb ...
Unpacking linux-headers-5.15.0-1030-aws (5.15.0-1030.34) ...
Preparing to unpack .../9-linux-headers-aws_5.15.0.1030.28_amd64.deb ...
Unpacking linux-headers-aws (5.15.0.1030.28) over (5.15.0.1028.26) ...
Setting up less (590-1ubuntu0.22.04.1) ...
Setting up linux-aws-headers-5.15.0-1030 (5.15.0-1030.34) ...
Setting up git-man (1:2.34.1-1ubuntu1.8) ...
Setting up linux-headers-5.15.0-1030-aws (5.15.0-1030.34) ...
Setting up linux-headers-aws (5.15.0.1030.28) ...
Setting up git (1:2.34.1-1ubuntu1.8) ...
Setting up linux-image-5.15.0-1030-aws (5.15.0-1030.34) ...
I: /boot/vmlinuz is now a symlink to vmlinuz-5.15.0-1030-aws
I: /boot/initrd.img is now a symlink to initrd.img-5.15.0-1030-aws
Setting up linux-image-aws (5.15.0.1030.28) ...
Setting up linux-modules-5.15.0-1030-aws (5.15.0-1030.34) ...
Setting up linux-aws (5.15.0.1030.28) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for linux-image-5.15.0-1030-aws (5.15.0-1030.34) ...
/etc/kernel/postinst.d/initramfs-tools:
update-initramfs: Generating /boot/initrd.img-5.15.0-1030-aws
/etc/kernel/postinst.d/zz-update-grub:
Sourcing file `/etc/default/grub'
Sourcing file `/etc/default/grub.d/40-force-partuuid.cfg'
Sourcing file `/etc/default/grub.d/50-cloudimg-settings.cfg'
Sourcing file `/etc/default/grub.d/init-select.cfg'
Generating grub configuration file ...
GRUB_FORCE_PARTUUID is set, will attempt initrdless boot
Found linux image: /boot/vmlinuz-5.15.0-1030-aws
Found initrd image: /boot/microcode.cpio /boot/initrd.img-5.15.0-1030-aws
Found linux image: /boot/vmlinuz-5.15.0-1028-aws
Found initrd image: /boot/microcode.cpio /boot/initrd.img-5.15.0-1028-aws
Warning: os-prober will not be executed to detect other bootable partitions.
Systems on them will not be added to the GRUB boot configuration.
Check GRUB_DISABLE_OS_PROBER documentation entry.
done
Scanning processes...
Scanning linux images...

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
ubuntu@ip-172-31-51-131:~$
ubuntu@ip-172-31-51-131:~$ curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -

## Installing the NodeSource Node.js 18.x repo...


## Populating apt-get cache...

+ apt-get update
Hit:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy InRelease
Hit:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates InRelease
Hit:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports InRelease
Hit:4 http://security.ubuntu.com/ubuntu jammy-security InRelease
Reading package lists... Done

## Confirming "jammy" is supported...

+ curl -sLf -o /dev/null 'https://deb.nodesource.com/node_18.x/dists/jammy/Release'

## Adding the NodeSource signing key to your keyring...

+ curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | gpg --dearmor | tee /usr/share/keyrings/nodesource.gpg >/dev/null

## Creating apt sources list file for the NodeSource Node.js 18.x repo...

+ echo 'deb [signed-by=/usr/share/keyrings/nodesource.gpg] https://deb.nodesource.com/node_18.x jammy main' > /etc/apt/sources.list.d/nodesource.list
+ echo 'deb-src [signed-by=/usr/share/keyrings/nodesource.gpg] https://deb.nodesource.com/node_18.x jammy main' >> /etc/apt/sources.list.d/nodesource.list

## Running `apt-get update` for you...

+ apt-get update
Hit:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy InRelease
Hit:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates InRelease
Hit:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports InRelease
Hit:4 http://security.ubuntu.com/ubuntu jammy-security InRelease
Get:5 https://deb.nodesource.com/node_18.x jammy InRelease [4563 B]
Get:6 https://deb.nodesource.com/node_18.x jammy/main amd64 Packages [774 B]
Fetched 5337 B in 1s (5310 B/s)
Reading package lists... Done

## Run `sudo apt-get install -y nodejs` to install Node.js 18.x and npm
## You may also need development tools to build native addons:
     sudo apt-get install gcc g++ make
## To install the Yarn package manager, run:
     curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --dearmor | sudo tee /usr/share/keyrings/yarnkey.gpg >/dev/null
     echo "deb [signed-by=/usr/share/keyrings/yarnkey.gpg] https://dl.yarnpkg.com/debian stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
     sudo apt-get update && sudo apt-get install yarn


ubuntu@ip-172-31-51-131:~$ sudo apt-get install -y nodejs
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following NEW packages will be installed:
  nodejs
0 upgraded, 1 newly installed, 0 to remove and 1 not upgraded.
Need to get 28.5 MB of archives.
After this operation, 186 MB of additional disk space will be used.
Get:1 https://deb.nodesource.com/node_18.x jammy/main amd64 nodejs amd64 18.14.0-deb-1nodesource1 [28.5 MB]
Fetched 28.5 MB in 0s (70.3 MB/s)
Selecting previously unselected package nodejs.
(Reading database ... 92360 files and directories currently installed.)
Preparing to unpack .../nodejs_18.14.0-deb-1nodesource1_amd64.deb ...
Unpacking nodejs (18.14.0-deb-1nodesource1) ...
Setting up nodejs (18.14.0-deb-1nodesource1) ...
Processing triggers for man-db (2.10.2-1) ...
Scanning processes...
Scanning linux images...

No services need to be restarted.
No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
ubuntu@ip-172-31-51-131:~$ node -v
v18.14.0
ubuntu@ip-172-31-51-131:~$ npm -v
9.3.1
ubuntu@ip-172-31-51-131:~$ mkdir Todo
ubuntu@ip-172-31-51-131:~$ ls
Todo
ubuntu@ip-172-31-51-131:~$ cd Todo
ubuntu@ip-172-31-51-131:~/Todo$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (todo)
version: (1.0.0)
description: A todo app
entry point: (index.js)
test command:
git repository:
keywords: todo application
author: Eze Onoky
license: (ISC)
About to write to /home/ubuntu/Todo/package.json:

{
  "name": "todo",
  "version": "1.0.0",
  "description": "A todo app",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "todo",
    "application"
  ],
  "author": "Eze Onoky",
  "license": "ISC"
}


Is this OK? (yes) yes
npm notice
npm notice New minor version of npm available! 9.3.1 -> 9.5.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v9.5.0
npm notice Run npm install -g npm@9.5.0 to update!
npm notice
ubuntu@ip-172-31-51-131:~/Todo$ ls
package.json
ubuntu@ip-172-31-51-131:~/Todo$

## INSTALL EXPRESSJS

Remember that Express is a framework for Node.js, therefore a lot of things developers would have programmed is already taken care of out of the box. Therefore it simplifies development, and abstracts a lot of low level details. For example, Express helps to define routes of your application based on HTTP methods and URLs.


ubuntu@ip-172-31-51-131:~/Todo$ npm install express

added 57 packages, and audited 58 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ touch index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ npm install dotenv

added 1 package, and audited 59 packages in 463ms

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
Server running on port 5000
ubuntu@ip-172-31-51-131:~/Todo$ mkdir routes
ubuntu@ip-172-31-51-131:~/Todo$ cd routes
ubuntu@ip-172-31-51-131:~/Todo/routes$ touch api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ vim api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ ubuntu@ip-172-31-51-131:~/Todo/routes$
ubuntu@ip-172-31-51-131:~/Todo/routes$

![PBL3_Picture2](https://user-images.githubusercontent.com/122687798/219301120-7c74adb6-144a-4567-a2c1-6a910670b2d7.JPG)

## MODELS

Now comes the interesting part, since the app is going to make use of Mongodb which is a NoSQL database, we need to create a model. A model is at the heart of JavaScript based applications, and it is what makes it interactive. We will also use models to define the database schema . This is important so that we will be able to define the fields stored in each Mongodb document.

In essence, the Schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database. These are known as virtual properties.To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier

ubuntu@ip-172-31-51-131:~/Todo$ npm install express

added 57 packages, and audited 58 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ touch index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ npm install dotenv

added 1 package, and audited 59 packages in 463ms

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
Server running on port 5000


mkdir routes
:qa
cd

sudo -i
curl -s http://169.254.169.254/latest/meta-data/public-ipv4
:q
q
exit
ubuntu@ip-172-31-51-131:~/Todo$ npm install express

added 57 packages, and audited 58 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ touch index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ npm install dotenv

added 1 package, and audited 59 packages in 463ms

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
Server running on port 5000ubuntu@ip-172-31-51-131:~/Todo$ npm install express

added 57 packages, and audited 58 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ touch index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ npm install dotenv

added 1 package, and audited 59 packages in 463ms

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
Server running on port 5000

ubuntu@ip-172-31-51-131:~/Todo$ npm install express

added 57 packages, and audited 58 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ touch index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ npm install dotenv

added 1 package, and audited 59 packages in 463ms

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ node index.js

ubuntu@ip-172-31-51-131:~/Todo$ npm install express

added 57 packages, and audited 58 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ touch index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ npm install dotenv

added 1 package, and audited 59 packages in 463ms

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
Server running on port 5000^C
ubuntu@ip-172-31-51-131:~/Todo$ mkdir routes
ubuntu@ip-172-31-51-131:~/Todo$ cd routes
ubuntu@ip-172-31-51-131:~/Todo/routes$ touch api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ vim api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ ubuntu@ip-172-31-51-131:~/Todo/routes$
ubuntu@ip-172-31-51-131:~/Todo/routes$ npm install mongoose

added 102 packages, and audited 161 packages in 6s

12 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo/routes$ cd
ubuntu@ip-172-31-51-131:~$ cd Todo/
ubuntu@ip-172-31-51-131:~/Todo$ npm install mongoose

up to date, audited 161 packages in 836ms

12 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ mkdir models
ubuntu@ip-172-31-51-131:~/Todo$ cd models
ubuntu@ip-172-31-51-131:~/Todo/models$ touch todo.js
ubuntu@ip-172-31-51-131:~/Todo/models$ ls
todo.js
ubuntu@ip-172-31-51-131:~/Todo/models$ vim todo.js
ubuntu@ip-172-31-51-131:~/Todo/models$ ubuntu@ip-172-31-51-131:~/Todo/models$
ubuntu@ip-172-31-51-131:~/Todo/models$
ubuntu@ip-172-31-51-131:~/Todo/models$ cat todo.js

const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
//const TodoSchema = new Schema({
//action: {
//type: String,
//required: [true, 'The todo text field is required']
//}
//})
//
////create model for todo
//const Todo = mongoose.model('todo', TodoSchema);
//
//module.exports = Todo;
ubuntu@ip-172-31-51-131:~/Todo/models$ ls
todo.js
ubuntu@ip-172-31-51-131:~/Todo/models$ cd
ubuntu@ip-172-31-51-131:~$ ls
Todo
ubuntu@ip-172-31-51-131:~$ cd Todo/
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  models  node_modules  package-lock.json  package.json  routes
ubuntu@ip-172-31-51-131:~/Todo$ cd routes/
ubuntu@ip-172-31-51-131:~/Todo/routes$ ls
api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ cat api.js

const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});


## MONGODB DATABASE

## Challenges Encountered
So there were alot of bugs on the script i ran earlier, attempts at server connection using node index.js command failed, util the bugs were removed. On Mongo DB, I was also unable to successfully connect from my windows terminal until i updated my current IP on the Mongo DB.

STEPS FOLLOWED...
We need a database where we will store our data. For this we will make use of mLab. mLab provides MongoDB database as a service solution (DBaaS), so to make life easy, you will need to sign up for a shared clusters free account, which is ideal for our use case.The signup process was followed.

PS C:\Users\EZEPC\Desktop\DevOps> ssh -i "PBL3_1.pem" ubuntu@ec2-54-160-80-149.compute-1.amazonaws.com
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-1030-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Fri Feb 17 02:12:27 UTC 2023

  System load:  0.0               Processes:             97
  Usage of /:   29.9% of 7.57GB   Users logged in:       1
  Memory usage: 21%               IPv4 address for eth0: 172.31.51.131
  Swap usage:   0%


 * Introducing Expanded Security Maintenance for Applications.
   Receive updates to over 25,000 software packages with your
   Ubuntu Pro subscription. Free for personal use.

     https://ubuntu.com/aws/pro

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


Last login: Fri Feb 17 00:20:37 2023 from 105.112.182.126
ubuntu@ip-172-31-51-131:~$
ubuntu@ip-172-31-51-131:~$
ubuntu@ip-172-31-51-131:~$
ubuntu@ip-172-31-51-131:~$ ls
Todo
ubuntu@ip-172-31-51-131:~$ cd Todo/
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  models  node_modules  package-lock.json  package.json  routes
ubuntu@ip-172-31-51-131:~/Todo$ cat todo.js
cat: todo.js: No such file or directory
ubuntu@ip-172-31-51-131:~/Todo$ cd models/
ubuntu@ip-172-31-51-131:~/Todo/models$ ls
todo.js
ubuntu@ip-172-31-51-131:~/Todo/models$ cat todo.js

const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
//const TodoSchema = new Schema({
//action: {
//type: String,
//required: [true, 'The todo text field is required']
//}
//})
//
////create model for todo
//const Todo = mongoose.model('todo', TodoSchema);
//
//module.exports = Todo;
ubuntu@ip-172-31-51-131:~/Todo/models$ vim todo.js
ubuntu@ip-172-31-51-131:~/Todo/models$ cd
ubuntu@ip-172-31-51-131:~$ cd Todo/
ubuntu@ip-172-31-51-131:~/Todo$ cd routes/
ubuntu@ip-172-31-51-131:~/Todo/routes$ ls
api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ vim api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ cd..

cd..: command not found
ubuntu@ip-172-31-51-131:~/Todo/routes$
ubuntu@ip-172-31-51-131:~/Todo/routes$ cd
ubuntu@ip-172-31-51-131:~$ cd Todo/
ubuntu@ip-172-31-51-131:~/Todo$ cat .env
DB = 'mongodb+srv://onokyeze:onoky@105.112.182.126/cluster0.o1a750v.mongodb.net?retryWrites=true&w=majority'
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  models  node_modules  package-lock.json  package.json  routes
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
(node:1228) [MONGOOSE] DeprecationWarning: Mongoose: the `strictQuery` option will be switched back to `false` by default in Mongoose 7. Use `mongoose.set('strictQuery', false);` if you want to prepare for this change. Or use `mongoose.set('strictQuery', true);` to suppress this warning.
(Use `node --trace-deprecation ...` to show where the warning was created)
Server running on port 5000
Error: querySrv ENOTFOUND _mongodb._tcp.105.112.182.126
    at QueryReqWrap.onresolve [as oncomplete] (node:internal/dns/promises:251:17) {
  errno: undefined,
  code: 'ENOTFOUND',
  syscall: 'querySrv',
  hostname: '_mongodb._tcp.105.112.182.126'
}
^C
ubuntu@ip-172-31-51-131:~/Todo$ cat .env
DB = 'mongodb+srv://onokyeze:onoky@105.112.182.126/cluster0.o1a750v.mongodb.net?retryWrites=true&w=majority'
ubuntu@ip-172-31-51-131:~/Todo$ vim .env
ubuntu@ip-172-31-51-131:~/Todo$ vim .env
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
(node:1243) [MONGOOSE] DeprecationWarning: Mongoose: the `strictQuery` option will be switched back to `false` by default in Mongoose 7. Use `mongoose.set('strictQuery', false);` if you want to prepare for this change. Or use `mongoose.set('strictQuery', true);` to suppress this warning.
(Use `node --trace-deprecation ...` to show where the warning was created)
Server running on port 5000
MongooseServerSelectionError: Could not connect to any servers in your MongoDB Atlas cluster. One common reason is that you're trying to access the database from an IP that isn't whitelisted. Make sure your current IP address is on your Atlas cluster's IP whitelist: https://docs.atlas.mongodb.com/security-whitelist/
    at Connection.openUri (/home/ubuntu/Todo/node_modules/mongoose/lib/connection.js:825:32)
    at /home/ubuntu/Todo/node_modules/mongoose/lib/index.js:411:10
    at /home/ubuntu/Todo/node_modules/mongoose/lib/helpers/promiseOrCallback.js:41:5
    at new Promise (<anonymous>)
    at promiseOrCallback (/home/ubuntu/Todo/node_modules/mongoose/lib/helpers/promiseOrCallback.js:40:10)
    at Mongoose._promiseOrCallback (/home/ubuntu/Todo/node_modules/mongoose/lib/index.js:1285:10)
    at Mongoose.connect (/home/ubuntu/Todo/node_modules/mongoose/lib/index.js:410:20)
    at Object.<anonymous> (/home/ubuntu/Todo/index.js:12:10)
    at Module._compile (node:internal/modules/cjs/loader:1226:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1280:10) {
  reason: TopologyDescription {
    type: 'ReplicaSetNoPrimary',
    servers: Map(3) {
      'ac-1ujm473-shard-00-01.o1a750v.mongodb.net:27017' => [ServerDescription],
      'ac-1ujm473-shard-00-02.o1a750v.mongodb.net:27017' => [ServerDescription],
      'ac-1ujm473-shard-00-00.o1a750v.mongodb.net:27017' => [ServerDescription]
    },
    stale: false,
    compatible: true,
    heartbeatFrequencyMS: 10000,
    localThresholdMS: 15,
    setName: 'atlas-1390n2-shard-0',
    maxElectionId: null,
    maxSetVersion: null,
    commonWireVersion: 0,
    logicalSessionTimeoutMinutes: null
  },
  code: undefined
}
^C
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
(node:1257) [MONGOOSE] DeprecationWarning: Mongoose: the `strictQuery` option will be switched back to `false` by default in Mongoose 7. Use `mongoose.set('strictQuery', false);` if you want to prepare for this change. Or use `mongoose.set('strictQuery', true);` to suppress this warning.
(Use `node --trace-deprecation ...` to show where the warning was created)
Server running on port 5000
Database connected successfully
