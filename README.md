# Boot repair in Ubuntu

```cmd
sudo add-apt-repository ppa:yannubuntu/boot-repair

sudo apt-get update

sudo apt-get install -y boot-repair

boot-repair
```

# Instalations

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