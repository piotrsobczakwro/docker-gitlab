# GITLAB 

GitLab CI/CD is the part of GitLab that you use for all of the continuous methods (Continuous Integration, Delivery, and Deployment). With GitLab CI/CD, you can test, build, and publish your code with no third-party application or integration needed.


## Enable podman registry
* Enable local registry  `podman run -d -p 5000:5000 --restart=always --name registry registry:2`
![image](https://user-images.githubusercontent.com/86531003/212487339-85a48ca6-08b7-4411-b9d8-57f4ff6e61f5.png)

* Pull image from dockerhub to your local registry `podman pull httpd`
![image](https://user-images.githubusercontent.com/86531003/212487377-3e06eab3-d289-4e52-bbe0-67f189fb5723.png)
  

`podman tag httpd localhost:5000/my-httpd` 

`podman run -dt -p 8080:80 localhost:5000/my-httpd` 

After commnads:

![image](https://user-images.githubusercontent.com/86531003/212488141-a214acb2-af74-4667-873f-d24f8dcc9382.png)


## Deploy gitlab on podman

* Installation of podman
  * `yum install podman -y`
  *  `podman ps`

* Deploy podman:
 ```
 # Create variable
 export GITLAB_HOME=/srv
 
 # Create paths 
 mkdir -p $GITLAB_HOME/gitlab/{config,logs,data}
 
 #  Run container
 podman run --detach \
  --privileged \
  --hostname gitlab.lab.local \
  --publish 443:443 --publish 80:80 --publish 55466:22 \
  --name gitlab \
  --restart always \
  --volume $GITLAB_HOME/gitlab/config:/etc/gitlab \
  --volume $GITLAB_HOME/gitlab/logs:/var/log/gitlab \
  --volume $GITLAB_HOME/gitlab/data:/var/opt/gitlab \
  gitlab/gitlab-ce:latest
 ```



## Links
* https://gitlab.com/gitlab-org/omnibus-gitlab/-/tree/master/files/gitlab-config-template

## Change password for root

https://docs.gitlab.com/ee/security/reset_user_password.html# docker-gitlab



## Install gitlab runner
```
# Download and install binary

 Download the binary for your system
sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64

# Give it permission to execute
sudo chmod +x /usr/local/bin/gitlab-runner

# Create a GitLab Runner user
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash

# Install and run as a service
sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
sudo gitlab-runner start

Command to register runner

sudo gitlab-runner register --url http://gitlab.lab.local/ --registration-token 3DyeHxUJz1crBdmRXHnm
```


## Install minkikube

https://minikube.sigs.k8s.io/docs/drivers/podman/

* Install the latest Minikube package
```
# Download package
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

# Change that file can be executed
chmod +x minikube-linux-amd64

# move that file to path
sudo mv minikube-linux-amd64 /usr/local/bin/minikube

#
```
root@vm-gitlab ~]# minikube start --driver=podman
😄  minikube v1.28.0 on Rocky 8.7 (kvm/amd64)
✨  Using the podman driver based on user configuration
🛑  The "podman" driver should not be used with root privileges. If you wish to continue as root, use --force.
💡  If you are running minikube within a VM, consider using --driver=none:
📘    https://minikube.sigs.k8s.io/docs/reference/drivers/none/

❌  Exiting due to DRV_AS_ROOT: The "podman" driver should not be used with root privileges.

```
```

Using force instead.
minikube start --driver=podman --force


```

