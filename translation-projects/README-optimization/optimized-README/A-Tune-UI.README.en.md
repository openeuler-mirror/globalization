English | [简体中文](./README.md)

## Introduction

**A-Tune-UI** is a visual Web interface. We use it in  [A-Tune](https://gitee.com/openeuler/A-Tune) projects, and it supports for openEuler-20.09 and higher versions.



## Installation & Usage

### Approach #1: Local installation and uasge

#### 1. Preparation

Remember that some required packages for UI such as nodejs and npm only exist in openeuler-everything.iso.  
Before installing, you should add openeuler-everything to your yum repo:  

1. Open [openeuler.org](https://openeuler.org/en/), click  `download`, then find corresponding iso and click  `download`again.   
2. Click `everything`, then choose corresponding version (`x86_64/aarch64`), and the page address should be the url used in yum configuration.  
3. Use url to add a yum repo. 

#### 2. Installation

#### 2-1. Installation using shell script

```bash
sh install.sh
```

This script will clone node-sass from gitee by default, but user can also change the url of node-sass package, taking github for example:
```bash
sh install.sh [git_url]
# for example, you can use github url to clone code
# sh install.sh https://github.com/sass/node-sass.git
```

> If installation failed, please follow the manual installation.


#### 2-2. Manual installation

##### 1) Install dependent system software packages

```bash
yum install -y npm nodejs gcc-c++ make patch
```

##### 2) Install dependent packages for NPM

```bash
npm ci
```
##### 3) Compile node-sass 

```bash
git clone -b v5 --recursive https://github.com/sass/node-sass.git
cd node-sass
git am arm-support.patch
npm i
node scripts/build -f
```

##### 4) Move node-sass into A-Tune-UI

```bash
mv node-sass A-Tune-UI/node_modules
```

#### 3. (Optional) Change the IP address

If your web page can not open in localhost, please change web IP address as follow:

```bash
hostname -I  # To get host IP
```
Open 'package.json' file, and replace 'localhost' with your host IP in line 10.

#### 4. Running

```bash
npm run start
```
This command will help you return to the website and open it.

Notes: This project is still in development stage, so any troubles in installation or running, please refer to Chapter 4 of The Practice Guide of A-Tune-UI. If your trouble still can not be resolved, please write Issue in repo.


### Approach #2: Installation and usage of docker image

#### 1. Preparation

Before installing, make sure that docker and wget tools have already been installed (no need to get all the repository, just get the Dockerfile):
```bash
yum install -y docker wget
wget https://gitee.com/openeuler/A-Tune-UI/Dockerfile
```

#### 2. Generation of atune-ui docker image

```bash
docker build --network=host -t atune-ui:latest .
```

#### 3. Running docker

```bash
docker run -p <local_ip>:<local_port>:8080 -e ENG_HOST=<engine-host> -e ENG_PORT=<engine-port> atune-ui
```

Notes:
- 'local_ip' is your Ip address, and 'local_port' is port that not been used. After running successfully, you can open web page by url: http://<local_ip>:<local_port>.
- 'engine-host' and 'engine-port' respectively correspond to ip and port info that you have set in A-Tune engine.cnf file.

> Notes: If A-Tune is not running, you can still get the web page but no data on it.


## Related Information

##### A-Tune
A-Tune project address: https://gitee.com/openeuler/A-Tune

##### A-Tune-Collector
A-Tune-Collector project address: https://gitee.com/openeuler/A-Tune-Collector

