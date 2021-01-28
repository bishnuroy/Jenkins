### Jenkins Operetor POC


**Operator Image:**
  - image: virtuslab/jenkins-operator:v0.4.0
  
**BackupImage**
  - image: virtuslab/jenkins-operator-backup-pvc:v0.1.0
  
**JenkinsImage**
  - image: jenkins/jenkins:lts
 

Base Plugin Version details:
```
 basePlugins: 
    - name: kubernetes
      version: 1.25.2
    - name: workflow-job
      version: "2.39"
    - name: workflow-aggregator
      version: "2.6"
    - name: git
      version: 4.2.2
    - name: job-dsl
      version: "1.77"
    - name: configuration-as-code
      version: "1.39"
      #version: "1.43"
      #version: "1.42"
    - name: configuration-as-code-support
      version: "1.19"
    - name: kubernetes-credentials-provider
      version: "0.13"
    - name: ldap
      version: "1.24"
    - name: pipeline-build-step
      version: "2.12"
    - name: pipeline-github
      version: "2.5"
    - name: config-file-provider
      version: "3.6.3"
    - name: matrix-auth 
      version: "2.6.2"
    - name: monitoring
      version: "1.82.0"
```

**Jenkins Ldap:** Change the LDAP ACL and give read attributes(except the password) access to the user. 
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: jenkins-testjk01-ldap
  labels:
    app: jenkins-operator
    jenkins-cr: jenkins-testjk01
data:
  jenkins-ldap-cm.yaml: |
    jenkins:
      systemMessage: "LDAP configured"
      securityRealm:
        ldap:
          configurations:
            - server: "ldap-server"
              groupMembershipStrategy: 
                #fromGroupSearch:
                fromUserRecord:
                   attributeName: "member"
                   #filter: "cn=test" 
              rootDN: "ou=test01,ou=br,o=example.com"
              userSearchBase: "ou=People"
              userSearch: "uid={0}"
              groupSearchBase: "ou=Group"
              groupSearchFilter: "objectClass=posixGroup"
              managerDN: "cn=Operator,ou=br,o=example.com"
              managerPasswordSecret: "Ldap-Operator-Password-PlainText"
              displayNameAttributeName: "cn"
              mailAddressAttributeName: "mail"
              ignoreIfUnavailable: "true"
          cache:
            size: 100
            ttl: 10
          userIdStrategy: CaseInsensitive
          groupIdStrategy: CaseSensitive
```

**BackUp:**

Here I have tested with VMDK dynamic storage.

