# MusicBox website
This website hosts information as well as firmware for the MusicBox product.

## Docker Deployment:
    * sudo apt update
    * sudo git clone <>
    * sudo nano .env on the server!
    * cd into source code (where compose and caddyfile are)

    * sudo curl -fsSL https://get.docker.com -o get-docker.sh
    * sudo sh get-docker.sh
    * sudo docker compose up

### Modify server service
    * sudo docker compose down
    * sudo docker rmi source_code-server
    <service the file> ex reset images * sudo rm -rf images/*
    * sudo docker compose up

### Modify via file replacement
    * sudo rm -rf <file>
    * sudo nano <file>
    * CTRL+O, CTRL+X
    * pm2 restart <app.file>

    NOTE can auto restart on file changes; 
    * pm2 start app.js --watch

	

## Standard ec2 Deployment:
    sudo apt update
    curl -fsSL https://deb.nodesource.com/setup_19.x | sudo -E bash - &&\sudo apt-get install -y nodejs
	sudo npm install pm2@latest -g
	sudo npm install serve


Sudo git pull (in root)
#### In server:
	sudo npm I
	sudo pm2 start ./bin/www
* (Maybe sudo pm2 deploy ./bin/www)? i made the deploy script use node whereas start probably still uses nodemon

#### In client:
	sudo npm i
	sudo npm run build
	sudo pm2 serve build 3000 -spa

## Useful procedures

### Check process locking port
    sudo lsof -i tcp:<port>
    sudo ps -faux (if previous command shows nothing, this will show the parent process spawning the locking child)
    kill -3 <pid>

### Make a change:
    sudo pm2 stop all
    sudo pm2 delete all

## Useful local database commands

### Setup local database on macOS
    brew tap mongodb/brew
    brew install mongodb-community@4.4  
    echo 'export PATH="/usr/local/opt/mongodb-community@4.4/bin:$PATH"' >> ~/.zshrc

### Start in terminal
    /usr/local/opt/mongodb-community@4.4/bin/mongod --config /usr/local/etc/mongod.conf
* Or, start as background service
    brew services start mongodb/brew/mongodb-community

### Connect from another terminal
    cd /usr/local/opt/mongodb-community@4.4
    ./bin/mongo