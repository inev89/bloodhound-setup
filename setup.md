# Bloodhound Setup

## Make a Bloodhound Directory
> [!NOTE] 
> Make a bloodhound directory, this can be in home.. but it will house your bloodhound install files and docker compose files

```
cd
mkdir bloodhound
cd bloodhound
```

## Download Bloodhound CLI

```
wget https://github.com/SpecterOps/bloodhound-cli/releases/latest/download/bloodhound-cli-linux-amd64.tar.gz
```

## Extract it
```
tar -xvzf bloodhound-cli-linux-amd64.tar.gz
```

## Run Bloodhound-CLI Install
> [!NOTE] 
> When you initially run the bloodhound-cli install, it will take over a few ports, importantly the 8080 Burp Proxy port... so make sure burp is not running, and then we can change the port after the install. If you are receiving docker errors, go to the docker section of this.

```
./bloodhound-cli install
```

## Tear Down Docker Instance

```
docker compose down
```

## Create Environment File

1) Create a .env file if you want to change the port bloodhound listens on

        touch .env
        vim .env

        #Add this to the .env file

        BH_API_PORT=8085
        BLOODHOUND_PORT=8085

## Spin up docker instance

```
docker compose up -d
```

## Browse to Login

```
http://127.0.0.1:8085/ui/explore
```

Done! Only go to the docker section if you haven't installed Docker on Kali yet.

# Installing Docker on Kali

```
sudo apt install -y docker.io
sudo apt install docker-compose
```

## Add current user to docker group

```
sudo usermod -aG docker $USER
newgrp docker
```

