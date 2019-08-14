# QA-community-201909
For thoughtworks(wuhan) QA-community-201909


###  install docker

**Mac**
待补充

**Windows**
待补充

### install jenkins
ref: https://jenkins.io/doc/book/installing/

```bash
docker run -d  --name tw-jenkins \
-p 8080:8080 \
-v /var/run/docker.sock:/var/run/docker.sock \
-v $PWD/jenkins:/var/jenkins_home \
jenkins/jenkins:2.184
```
![](images/jenkins_setup_02.png)

`docker exec -it -u root tw-jenkins bash`

```bash
chmod 755 /var/run/docker.sock
apt-get update && \
apt-get -y install apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common && \
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable" && \
apt-get update && \
apt-get -y install docker-ce
```

wait: 5min

### install sonarqube

ref: https://docs.docker.com/samples/library/sonarqube/

docker pull sonarqube:7.8-community

docker run -d --name tw-sonarqube -p 9000:9000 sonarqube:7.8-community

// wait 5s,

In the window above, please click the Login button to login to the administrator account of SonarQube with “admin” username and password is also “admin”.

##### install sonar scanner
https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/


sonar  页面安装插件
jenkins  安装插件
- pipeline
- gitlab

doc ref: https://github.com/ValaxyTech/DevOpsDemos/blob/master/SonarQube/Sonar_Integration_with_Jenkins.MD
https://www.youtube.com/watch?v=k-3krTRuAFA
