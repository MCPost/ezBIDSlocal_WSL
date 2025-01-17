# ezBIDSlocal_WSL
A step-by-step instruction to use ezBIDS locally via Docker and WSL2 (Windows Subsystem for Linux 2)

The easiest way to set it up is to install Docker not on Windows (e.g. as Docker Desktop) but on the Windows Subsystem for Linux.


## 1. Install WSL and Ubuntu
WSL can be easily installed in Windows by opening a command window (type cmd in the search bar) or a powershell window and type:

```posh
wsl --install
```


## 2. Install Docker Engine and Compose on WSL

After installing WSL2 and a Linux distribution (e.g. Ubuntu) you can activate it by typing `wsl`. Now you should be in a linux bash environment.
The steps for installing Docker and Docker compose on the WSL are taken from this [post](https://dev.to/felipecrs/simply-run-docker-on-wsl2-3o8) by Felipe Santos.

Ensures not older packages are installed
```sh
sudo apt-get remove docker docker-engine docker.io containerd runc
```

Ensure pre-requisites are installed (added make and g++ from previous instructions)
```sh
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release make g++
```

Adds docker apt key
```sh
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

Adds docker apt repository
```sh
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
 $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Refreshes apt repos
```sh
sudo apt-get update
```

Installs Docker CE
```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## 3. Install node.js and npm

Generally, you can follow the instruction given [here](https://nodejs.org/en/download/). Be sure to choose "for Linux".
First install the fmn package manager for node.js
```sh
curl -o- https://fnm.vercel.app/install | bash
```
Now install the node.js version 20.11.0 as suggested in the [ezBIDS documentation](https://brainlife.io/docs/using_ezBIDS/#installing-ezbids-locally)
```sh
fnm install 20.11.0
```
You can check now that node and npm are the correct versions
```sh
node -v  # should print "20.11.0"
npm -v   # should print "10.2.4"
```

## 4. Download and Setup the ezBIDS container

From this point on you can follow the [ezBIDS documentation](https://brainlife.io/docs/using_ezBIDS/#installing-ezbids-locally) from "Step 2: Setup" onwards. 
First, you have to clone the ezBIDS github repo and then use the dev.sh file to set up the Docker container needed.
```sh
git clone https://github.com/brainlife/ezbids.git
cd ezbids && ./dev.sh -d
```
Now the docker container is running in the current terminal. It will print a local address like `http://localhost:3000/ezbids/convert`. Paste this into your internet browser which should open up the ezBIDS website locally. Now you can use ezBIDS locally.

