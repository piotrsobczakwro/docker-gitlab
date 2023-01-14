# GITLAB 

GitLab CI/CD is the part of GitLab that you use for all of the continuous methods (Continuous Integration, Delivery, and Deployment). With GitLab CI/CD, you can test, build, and publish your code with no third-party application or integration needed.


## Enable podman registry


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

Download and install binary

# Download the binary for your system
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
