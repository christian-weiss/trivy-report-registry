# Setup A GCP Server

## Preparations
- register an account at GCP
- login into your GCP account at https://console.cloud.google.com/

# Create VM instance
- click on "Compute Engine" / "Create instance"
- select
  - "Region" = e.g. "us-east1" 
  - "Machine type" = "fi-micro" (this machine type is maybe not available in all regions)
  - "Boot Disk" = "ubuntu-minimal-1804-bionic-v20191024"
  - "Allow HTTP traffic" = checked
  - "Allow HTTPS traffic" = checked
- click on "create"

# Enable swap
``` 
# create swap
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

#verify with top
top
```

# Make swap settings persistent
```
# install vi
sudo apt-get update
sudo apt install -y vi
sudo vi /etc/fstab
```
Add the following line to then end of the file:
```
/swapfile none swap sw 0 0 
# save with ESC + ":" + "w" + "q" + ENTER
```

# Install docker
```
curl https://get.docker.com > install-docker.sh
chmod 755 install-docker.sh
./install-docker.sh
# replace "nameHere" with your user name
sudo usermod -aG docker nameHere
# verify
docker --version
``` 

# Install docker-compose
``` 
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod 755 /usr/local/bin/docker-compose
#verify
docker-compose --version
```

# Test your domain (DNS)
``` 
docker run --rm -p 80:80 strm/helloworld-http
# enter your domain name in a new browser tab
# you should now see the "hello world"

# stop the helloworld-http with CTRL+C
```

# What next?
See [how to install TRR](INSTALL.md)

