# Install and Configure Maven & git in Jenkins server

## Install Maven
```
yum install wget
wget https://dlcdn.apache.org/maven/maven-3/3.9.1/binaries/apache-maven-3.9.1-bin.tar.gz

# update ~/.bash_profile with below
M2_HOME=/opt/apache-maven-3.9.1
M2=/opt/apache-maven-3.9.1/bin
export M2_HOME
export M2
PATH=$PATH:$M2

# To set it permanently update your .bash_profile
source ~/.bash_profile

#Validate Maven
mvn version
```

## Install git
```sh
yum install git
```

## Assign shell to jenkins user

```sh
vi /etc/passwd
change shell from /bin/false to /bin/bash
```

