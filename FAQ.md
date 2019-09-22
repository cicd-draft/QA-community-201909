### **Q1: windows docker 启动后本地无法访问 localhost:端口**
A: 
  If you’re using Docker Toolbox then any port you publish with docker run -p will be published on the Toolbox VM’s private IP address. docker-machine ip will tell you. It is frequently 192.168.99.100.
  
  在安装了一个Windows下安装了docker，并尝试在其中运行Nginx服务，但映射完毕之后，在主机的浏览器中，打开localhost:port无法访问对应的服务。
  
**原因**：docker是运行在Linux上的，在Windows中运行docker，实际上还是在Windows下先安装了一个Linux环境，然后在这个系统中运行的docker。也就是说，服务中使用的localhost指的是这个Linux环境的地址，而不是我们的宿主环境Windows。
  找到这个Linux的ip地址，一般情况下这个地址是 **192.168.99.100**（docker-machine ip default 命令查找）
  
  
### **Q2: 国内拉取 docker 镜像慢**
  
换国内镜像仓库地址 (启动容器时也需要使用对应的镜像名称)
```bash
##使用 aliyun 镜像仓库
docker pull registry.cn-hangzhou.aliyuncs.com/cicddraft/jenkins:v0.4
docker pull registry.cn-hangzhou.aliyuncs.com/cicddraft/sonarqube:7.8-community
```
  
参考：
  - https://blog.csdn.net/IT_xiao_bai/article/details/83070070
  - http://frankchen.xyz/2017/02/17/Docker-Windows-Speed-up/


### **Q3: sonarqube 异常退出 （SonarQube Process(docker container) exited with exit value [es]: 137**）
A: 
There's a memory limit of 2GB(by default).If you are using docker-for-windows or docker-for-mac you can easily increase it from the Whale 🐳 icon in the task bar, then go to Preferences -> Advanced:.Remember to apply the ram limit increase changes. Restart the docker
`docker stats`

```bash
docker run -d -m=4g --name tw-sonarqube -p 9000:9000 sonarqube:7.8-community
```

```bash
docker run -d sonarqube -Dsonar.ce.javaOpts=-Xmx2048m -Dsonar.web.javaOpts=-Xmx2048m
```
> http://forum.cakewalk.com/Why-does-Sonar-run-out-of-memory-m340719.aspx
