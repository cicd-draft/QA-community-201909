<h4 style="color: red;">Only for non-production environment</h4>

# QA-community-201909
For thoughtworks(wuhan) QA-community-201909

**Stack**: git, jenkins, docker, sonarqube

![](images/arch_01.png)


目的： 利用 docker 本地搭建CI/CD 环境，并执行 单元测试，集成测试，代码扫描等步骤，最后部署在本地

###  1.安装docker

- **Mac**
[install on mac](https://docs.docker.com/v17.12/docker-for-mac/install/#download-docker-for-mac)

- **Windows**
[install on windows](https://docs.docker.com/docker-for-windows/install/)

> **wait: 10m**

获取镜像到本地：
```bash
docker pull sonarqube:7.8-community
docker pull cicddraft/jenkins:v0.4
```

如有网络原因，可采取导入本地镜像包
```bash
docker load < my_image.tar
docker images 
```

### 2.安装 jenkins

启动Jenkins
>Start the container with mounted docker daemon
```bash
docker run --name tw-jcasc -d    \
-p 8081:8080   \
-v /var/run/docker.sock:/var/run/docker.sock \
cicddraft/jenkins:v0.4
```
> **wait: 5s**

### 3.安装 sonarqube

>ref: https://docs.docker.com/samples/library/sonarqube/

启动sonarqube:

`docker run -d --name tw-sonarqube -p 9000:9000 sonarqube:7.8-community`

> **wait 5s**

In the window above, please click the Login button to login to the administrator account of SonarQube with “admin” username and password is also “admin”.

### 4.新建jenkins job,并运行

##### 4.1 本地运行

`git clone  https://github.com/lewisice/api-test-demo`

见 https://github.com/lewisice/api-test-demo

##### 4.2 新建一个 Freestyle 类型的job


##### 4.3 Pipeline as code ,新建 pipeline 类型job  
"jenkins" --> "New Item"  

<img alt="xxx" src="images/jenkins_setup_04.png" valigin="middle" height="400"/>

<img alt="xxx" src="images/browser_screenshot_1.png" valigin="middle" height="200"/>

![](images/sonarqube_01.png)

---
what's more:
https://github.com/qinrui777/sonarqube-metric-to-grafana


<img src="images/sonar_to_grafana.png" width="380" height="220" >      <img src="images/jenkins_to_grafana.png" width="380" height="220" >
