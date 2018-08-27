# Jenkins

Ref: https://github.com/jenkinsci/docker


1. JENKINS_HOME=/var/jenkins_home (Jenkind Home Dirctory:)

2. Mount this path for PVS: "/var/jenkins_home" 

3. Admin Pass word will be store in : /var/jenkins_home/secrets/initialAdminPassword In this file.

4. Docker Build:

```
   docker build -t jenkins-2.121.3 .
```
5. Docker Run:

```
docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins-2.121.3
```

Reset the admin password.
