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

Done!

# Installing Docker on Kali
> [!NOTE]
> This is only required if you are unable to run ./bloodhound-cli. Try to use sudo with it first, if it doesn't work then proceed.

```
sudo apt install -y docker.io
sudo apt install docker-compose
```

## Add current user to docker group
> [!NOTE]
> You may need to do this unless you want to use 'sudo' with every ./bloodhound-cli or docker command.

```
sudo usermod -aG docker $USER
newgrp docker
```

# Troubleshooting
If bloodhound is not running, confirm it with

```
docker ps
```

Once you confirmed it is not running, you need to restart the docker containers.

```
cd ~/bloodhound
docker compose restart
```

If those containers do not exist, you can create new ones with
```
cd ~/bloodhound
docker compose up -d
```

# Ease of Use
You can create an easy script that will check to see if bloodhound is running and pull up a browser or restart bloodhound. I created this file below and added it to `/home/kali/.local/bin` so you can just type in bloodhound. Make sure to delete your bash cache by running `hash -r`

```
vim /home/kali/.local/bin/bloodhound
```

```
if docker ps --format '{{.Names}}' | grep -q "bloodhound-bloodhound"; then 
        echo "Containers are live. Bringing up Firefox"
        firefox "http://127.0.0.1:8085/ui/login" &
else
        echo "Container is not running. Restarting."
        cd ~/bloodhound && docker compose down && docker compose up -d
        firefox "http://127.0.0.1:8085/ui/login" &
fi
```

```
chmod +x /home/kali/.local/bin/bloodhound
hash -r
```



