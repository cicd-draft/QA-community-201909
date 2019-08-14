#### **Q: SonarQube Process(docker container) exited with exit value [es]: 137**
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