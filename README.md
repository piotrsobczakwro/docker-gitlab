# GITLAB 


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
