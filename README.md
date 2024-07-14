# Deploy .Net Web API Service using Docker on Ubuntu

## Install Docker

### Step 1: Update and Upgrade Packages

#### First, update your existing list of packages:

```bash
sudo apt update
```
#### Then, upgrade the installed packages to the latest versions:

```bash
sudo apt upgrade
```

### Step 2: Install apt-utils

#### Install apt-utils to ensure smooth package installations:

```bash
sudo apt-get install -y apt-utils
```

### Step 3: Install Docker

#### Install Docker from the default Ubuntu repositories:

```bash
sudo apt install -y docker.io
```

### Step 4: Start and Enable Docker

#### Start the Docker service:

```bash
sudo systemctl start docker
```

#### Enable Docker to start on boot:

```bash
sudo systemctl enable docker
```

### Step 5: Add Your User to the Docker Group

#### To avoid needing sudo for every Docker command, add your user to the docker group:

```bash
sudo usermod -aG docker $USER
```

##### Replace $USER with your actual username (i.e. ubuntu) if necessary.

### Step 6: Log Out and Log Back In

#### Log out and log back in to apply the changes to your user group.

### Step 7: Verify Docker Installation

#### Check the Docker version to ensure it is installed correctly:

```bash
docker --version
```

### Step 8: Check Docker Service Status

#### Verify that the Docker service is running:

```bash
sudo systemctl status docker
```

### Step 9: Enable Docker Service to Start on Boot (if needed)

#### If not already done, ensure Docker starts on boot:

```bash
sudo systemctl enable docker
```

### Step 10: Run a Test Container

#### Finally, run a test container to verify that Docker is working correctly:

```bash
docker run hello-world
```

##### This command pulls the hello-world image from Docker Hub and runs it in a container. You should see a message that confirms Docker is installed and running correctly.

## Deploy Application

### Step 1: Clone the app

#### Clone the app to get the source codes:

```bash
git clone https://github.com/awsaf-utm/Deploy-.Net-Web-API-Service-using-Docker-on-Ubuntu.git
```

### Step 2: Go to the app folder

#### To get solution (.sln) file of the application:

```bash
cd Deploy-.Net-Web-API-Service-using-Docker-on-Ubuntu/BookInformationService
```

### Step 3: Install dependencies

#### Install the dependencies:

```bash
dotnet restore
```

### Step 4: Publish the Project

#### To release in the out folder:

```bash
dotnet publish -c Release -o out
```

### Step 5: Add port

#### To access the port 3101:

```bash
sudo ufw allow 3101/tcp
```

### Step 6: Restart firewall

#### To affect the changes:

```bash
sudo ufw reload
```

### Step 7: Check status

#### To verify:

```bash
sudo ufw status
```

## Run Application on Docker 

### Step 1: Build Docker Image

#### Build the Docker image to run on Docker Container:

```bash
docker build --build-arg ENVIRONMENT=Development -t engzaman2020/book-info-svc:1 .
```

### Step 2: Run Docker Image

#### Build the Docker image to run on Docker Container:

```bash
docker run -it -p 8101:3101 -e ENVIRONMENT=Development engzaman2020/book-info-svc:1
```

## Access from host OS 

### Step 1: Build Docker Image

#### Find the physical network interface card (NIC) on the host:

##### Note: Physical NICs often have names that start with en (Ethernet) or eth (Ethernet) followed by a number (e.g., enp0s3, eth0).

```bash
ifconfig
```

##### And

```bash
ip route
```

### Step 2: Use the Physical NIC to access from host OS

#### http://[Physical NIC]:8101/swagger/index.html

##### Example:

#### http://192.168.1.249:8101/swagger/index.html

