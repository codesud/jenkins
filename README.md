# jenkins

This is the repo which contains all the jenkins learning and CICD of our project


This is cron scheduler

```
cron('H */4 * * 1-5') 
```

Place dry-run effort in Jenkins


GitHUB uses Auth Token for Authorization ( Token is a string of encrypted userName and password )

### Jenkins intallation 

source : https://www.jenkins.io/doc/book/installing/linux/#red-hat-centos

Important, if you get error(ERROR: cannot verify pkg.jenkins.io's certificate, issued by ‘/C=US/O=Let's Encrypt/CN=R3’:
  Issued certificate has expired.) update the centos image by running below code and try again.
```
sudo yum update -y
```

