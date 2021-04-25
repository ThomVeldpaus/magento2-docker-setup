# symfony-docker-setup

## Start build 
docker-compose up -d --build

## elasticsearch settings
su thom
nano /home/thom/elasticsearch-7.12.0/config/elasticsearch.yml

# set the following
cluster.name: my-application
node.name: node-1
network.host: localhost
http.port: 9200

# start elasticsearch
cd ~/elasticsearch-7.12.0
./bin/elasticsearch

## Deploy sample data
cd /app
php bin/magento sampledata:deploy

## Install Magento 2
### WARNING: Sampledata will be installed, remove --use-sample-data if not needed:
php bin/magento setup:install --admin-firstname=thom --admin-lastname=Veldpaus --admin-email=thom@example.com  --admin-user=admin --admin-password='Admin123'  --base-url=https://local.domain.com --base-url-secure=https://local.domain.com --backend-frontname=admin --db-host=mysql --db-name=magento --db-user=root --db-password=root  --use-rewrites=1 --language=nl_NL --currency=EUR --timezone=Europe/Amsterdam --use-secure-admin=1 --admin-use-security-key=1 --session-save=files --use-sample-data


