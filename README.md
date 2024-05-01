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

## Integration with external gNB/UE in local
## Integracion with external gNB/UE in VM

To more information visit [Installing UERANSIM - a UE/RAN Simulator](https://free5gc.org/guide/5-install-ueransim/)

### Enviorament

Created a ubuntu-20.04 VM with a network adapter as bridge adapter and hostname **ueransim**
Start the VM and:

Verify conection:
```cmd
ping www.google.com
ip a
```

Verify the hostname **ueransim** in /etc/hostname and /etc/hosts files, edit them if is necesary:
```cmd
ubuntu@ueransim:/etc/netplan$ cat /etc/hostname
ueransim
ubuntu@ueransim:/etc/netplan$ cat /etc/hosts
127.0.0.1	localhost
127.0.1.1	ueransim

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

```

Config network adapters:
```cmd
cd /etc/netplan
sudo nano 00-installer-config.yaml
```

Copy it in ***nano 00-installer-config.yaml***
```cmd
network:
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
      dhcp4: no
      addresses: [192.168.21.131/24]
  version: 2
```

Apply de changes:
```cmd
sudo netplan try
sudo netplan apply
```

Verify conection with the host:
```cmd
ip a
ping 192.168.21.130 # ip del host
```

Install the next tools and packages:
- `sudo apt install git`

### Instalation

See de this tutorial to ueransin [instalation](https://github.com/aligungr/UERANSIM/wiki/Installation).

```cmd
cd ~
git clone https://github.com/aligungr/UERANSIM

sudo apt update
sudo apt upgrade # Optional

sudo apt install make
sudo apt install gcc
sudo apt install g++
sudo apt install libsctp-dev lksctp-tools
sudo apt install iproute2
sudo snap install cmake --classic

cd ~/UERANSIM
make
```

And that's it. After successfully compiling the project, output binaries will be copied to ~/UERANSIM/build folder. And you should see the following files:

nr-gnb | Main executable for 5G gNB (RAN)
nr-ue | Main executable for 5G UE
nr-cli | CLI tool for 5G gNB and UE
nr-binder | A tool for utilizing UE's internet connectivity.
libdevbnd.so | A dynamic library for nr-binder
Run nr-gnb and nr-ue to start using UE and gNB. More details about them can be found in next steps.

nr-binder and libdevbnd.so are only required for binding UEs internet connectivity to an arbitrary application, and generally not used.

### Setting Free5GC

If use a [Free5GC VM](https://free5gc.org/guide/2-config-vm-en/) follow the next steps:

Login in the Free5GC VM:
```cmd
sudo apt install openssh-server # In ueransim VM (guest)
ssh ssh [username]@[host_ip_address] - p [port] # In the host
```

Replace ngapIpList IP from amf.free5gc.org to 192.168.21.130 in **config/amfcfg.yaml**

In the entry inside userplaneInformation / upNodes / UPF / interfaces / endpoints, change the IP from upf.free5gc.org to 192.168.21.130 in **config/smfcfg.yaml**

Finally, edit **config/upfcfg.yaml**，and chage gtpu IP from upf.free5gc.org into 192.168.56.101

### Setting UERANSIM

You can see the UERANSIM [configuration](https://github.com/aligungr/UERANSIM/wiki/Configuration) and github [repository](https://github.com/aligungr/UERANSIM)

Login in the ueransim VM:
```cmd
sudo apt install openssh-server # In ueransim VM (guest)
ssh ssh [username]@[host_ip_address] - p [port] # In the host
ssh-keygen -f "/home/tesis/.ssh/known_hosts" -R "192.168.21.131" # Remove a entry of old host
```

In the ueransim VM, there are two files related to free5GC：

- ~/UERANSIM/config/free5gc-gnb.yaml
- ~/UERANSIM/config/free5gc-ue.yaml

The second file is for UE, which we don’t have to change if the data inside is consistent with the (default) registration data we set using WebConsole previously.

First SSH into ueransim, and edit the file ~/UERANSIM/config/free5gc-gnb.yaml, and change the ngapIp IP, as well as the gtpIp IP, from 127.0.0.1 to 192.168.21.131，and also change the IP in amfConfigs into 192.168.21.130

### Testing UERANSIM against free5GC

You can see the UERANSIM [usage](https://github.com/aligungr/UERANSIM/wiki/Usage).

SSH into free5gc. If you have rebooted free5gc, remember to run:
```cmd
sudo sysctl -w net.ipv4.ip_forward=1
sudo iptables -t nat -A POSTROUTING -o <dn_interface> -j MASQUERADE
sudo systemctl stop ufw
```

Note: In Ubuntu Server 20.04 and 22.04 the dn_interface may be called enp0s3 or enp0s4 by default. Use the command ip a to help to figure it out

In addition, execute the following command:
```cmd
sudo iptables -I FORWARD 1 -j ACCEPT
```

The last comands permit:
1. sudo sysctl -w net.ipv4.ip_forward=1: Habilita el reenvío de paquetes IP en el kernel del sistema, permitiendo que actúe como un enrutador.
2. sudo iptables -t nat -A POSTROUTING -o wlp3s0 -j MASQUERADE: Configura una regla de traducción de direcciones de red (NAT) para ocultar las direcciones IP internas detrás de la dirección IP de la interfaz de salida.
3. sudo systemctl stop ufw: Detiene el servicio de firewall ufw, desactivando cualquier regla de firewall que esté siendo aplicada.
4. sudo iptables -I FORWARD 1 -j ACCEPT: Inserta una regla en iptables para permitir el reenvío de paquetes entre interfaces de red, necesaria porque la política predeterminada bloquea estos paquetes.

Reboot free5GC if you change the config.

At this time free5GC has been started.

Next, prepare three additional SSH terminals from your host machine (if you know how to use tmux, you can use just one).

In terminal 1: SSH into ueransim, make sure UERANSIM is built, and configuration files have been changed correctly, then execute nr-gnb:
```cmd
cd ~/UERANSIM
build/nr-gnb -c config/free5gc-gnb.yaml
```

In terminal 2, SSH into ueransim, and execute nr-ue with admin right:
```cmd
cd ~/UERANSIM
sudo build/nr-ue -c config/free5gc-ue.yaml # for multiple-UEs, use -n and -t for number and delay
```

In terminal 3, SSH into ueransim, and ping 192.168.21.130 to see free5gc is alive. Then, use ifconfig to see if the tunnel uesimtun0 has been created (by nr-ue):
```cmd
ifconfig
```
