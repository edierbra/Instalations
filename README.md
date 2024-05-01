# Troubleshots

## Boot repair in Ubuntu

```cmd
sudo add-apt-repository ppa:yannubuntu/boot-repair

sudo apt-get update

sudo apt-get install -y boot-repair

boot-repair
```

# Tools (Optional)

## Install Brave Browser

```cmd
sudo apt install curl

sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list

sudo apt update

sudo apt install brave-browser
```
## Install Visual Code ([Link](https://linuxize.com/post/how-to-install-visual-studio-code-on-ubuntu-20-04/#:~:text=1%20Update%20the%20packages%20index%20and%20install%20the,Visual%20Studio%20Code%20package%3Asudo%20apt%20install...%20More%20))

```cmd
sudo snap install --classic code
```

## Install git

```cmd
sudo apt install git
```

To configure SSH on Git see the seccion **Configurar llaves SSH en local** in [this tutorial](https://github.com/edierbra/Cursos/tree/GitHub)

# Free5gc Compose ([Repository](https://github.com/free5gc/free5gc-compose/tree/v3.4.1))

## Prerequisities

### [GTP5G kernel module](https://github.com/free5gc/gtp5g): needed to run the UPF

We use [GTP5G v0.8.8](https://github.com/free5gc/gtp5g/tree/v0.8.8)

```cmd
git clone https://github.com/free5gc/gtp5g.git && cd gtp5g
make clean && make
sudo make install
```

### [Docker Engine](https://docs.docker.com/engine/install): to run the Free5GC containers and  [Docker Compose v2](https://docs.docker.com/compose/install): to bootstrap the free5GC stack

We use:
- Docker Compose version v2.26
- Docker Engine version v26.1.0

```cmd
# Run the following command to uninstall all conflicting packages
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done

# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# To install the latest version
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# To install a specific version (Optional)
# List the available versions:
apt-cache madison docker-ce | awk '{ print $3 }'
5:24.0.0-1~ubuntu.22.04~jammy
5:23.0.6-1~ubuntu.22.04~jammy
...
VERSION_STRING=5:24.0.0-1~ubuntu.22.04~jammy
sudo apt-get install docker-ce=$VERSION_STRING docker-ce-cli=$VERSION_STRING containerd.io docker-buildx-plugin docker-compose-plugin

# Verify that the Docker Engine installation is successful
sudo docker run hello-world
```

## Start free5gc

### Clone de Repository

We use [free5gc-compose v3.4.1](https://github.com/free5gc/free5gc-compose/tree/v3.4.1
)

```cmd
git clone https://github.com/free5gc/free5gc-compose.git
```

### Pull the images

```cmd
# Enter to the free5gc-compose proyect and run:
docker compose pull
```

### [Optional] Build docker images from local sources

```cmd
# Clone the project
git clone https://github.com/free5gc/free5gc-compose.git
cd free5gc-compose

# clone free5gc sources
cd base
git clone --recursive -j `nproc` https://github.com/free5gc/free5gc.git
cd ..

# Build the images
make all
docker compose -f docker-compose-build.yaml build

# Alternatively you can build specific NF image e.g.:
make amf
docker compose -f docker-compose-build.yaml build free5gc-amf
```

### Run free5GC

You can create free5GC containers based on local images or docker hub images:

#### use local images

```cmd
docker compose -f docker-compose-build.yaml up
```

#### use images from docker hub

```cmd
docker compose up # add -d to run in background mode
```

### Destroy the established container resource after testing:

#### Remove established containers (local images)

```cmd
docker compose -f docker-compose-build.yaml rm
```

#### Remove established containers (remote images)

```cmd
docker compose rm
```

## Integration with external gNB/UE

# Troubleshots

## Boot repair in Ubuntu

```cmd
sudo add-apt-repository ppa:yannubuntu/boot-repair

sudo apt-get update

sudo apt-get install -y boot-repair

boot-repair
```

# Tools (Optional)

## Install Brave Browser

```cmd
sudo apt install curl

sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list

sudo apt update

sudo apt install brave-browser
```
## Install Visual Code ([Link](https://linuxize.com/post/how-to-install-visual-studio-code-on-ubuntu-20-04/#:~:text=1%20Update%20the%20packages%20index%20and%20install%20the,Visual%20Studio%20Code%20package%3Asudo%20apt%20install...%20More%20))

```cmd
sudo snap install --classic code
```

## Install git

```cmd
sudo apt install git
```

To configure SSH on Git see the seccion **Configurar llaves SSH en local** in [this tutorial](https://github.com/edierbra/Cursos/tree/GitHub)

# Free5gc Compose ([Repository](https://github.com/free5gc/free5gc-compose/tree/v3.4.1))

## Prerequisities

### [GTP5G kernel module](https://github.com/free5gc/gtp5g): needed to run the UPF

We use [GTP5G v0.8.8](https://github.com/free5gc/gtp5g/tree/v0.8.8)

```cmd
git clone https://github.com/free5gc/gtp5g.git && cd gtp5g
make clean && make
sudo make install
```

### [Docker Engine](https://docs.docker.com/engine/install): to run the Free5GC containers and  [Docker Compose v2](https://docs.docker.com/compose/install): to bootstrap the free5GC stack

We use:
- Docker Compose version v2.26
- Docker Engine version v26.1.0

```cmd
# Run the following command to uninstall all conflicting packages
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done

# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# To install the latest version
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# To install a specific version (Optional)
# List the available versions:
apt-cache madison docker-ce | awk '{ print $3 }'
5:24.0.0-1~ubuntu.22.04~jammy
5:23.0.6-1~ubuntu.22.04~jammy
...
VERSION_STRING=5:24.0.0-1~ubuntu.22.04~jammy
sudo apt-get install docker-ce=$VERSION_STRING docker-ce-cli=$VERSION_STRING containerd.io docker-buildx-plugin docker-compose-plugin

# Verify that the Docker Engine installation is successful
sudo docker run hello-world
```

## Start free5gc

### Clone de Repository

We use [free5gc-compose v3.4.1](https://github.com/free5gc/free5gc-compose/tree/v3.4.1
)

```cmd
git clone https://github.com/free5gc/free5gc-compose.git
```

### Pull the images

```cmd
# Enter to the free5gc-compose proyect and run:
docker compose pull
```

### [Optional] Build docker images from local sources

```cmd
# Clone the project
git clone https://github.com/free5gc/free5gc-compose.git
cd free5gc-compose

# clone free5gc sources
cd base
git clone --recursive -j `nproc` https://github.com/free5gc/free5gc.git
cd ..

# Build the images
make all
docker compose -f docker-compose-build.yaml build

# Alternatively you can build specific NF image e.g.:
make amf
docker compose -f docker-compose-build.yaml build free5gc-amf
```

### Run free5GC

You can create free5GC containers based on local images or docker hub images:

#### use local images

```cmd
docker compose -f docker-compose-build.yaml up
```

#### use images from docker hub

```cmd
docker compose up # add -d to run in background mode
```

### Destroy the established container resource after testing:

#### Remove established containers (local images)

```cmd
docker compose -f docker-compose-build.yaml rm
```

#### Remove established containers (remote images)

```cmd
docker compose rm
```

## Integration with external gNB/UE
