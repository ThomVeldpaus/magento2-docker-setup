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

## pre install filepermissions
cd app  
find var generated vendor pub/static pub/media app/etc -type f -exec chmod u+w {} +  
find var generated vendor pub/static pub/media app/etc -type d -exec chmod u+w {} +  
chown -R thom:www-data .  
chmod u+x bin/magento  

## Install Magento 2
### WARNING: Sampledata will be installed, remove --use-sample-data if not needed:
su thom
php bin/magento setup:install --admin-firstname=thom --admin-lastname=Veldpaus --admin-email=thom@example.com  --admin-user=admin --admin-password='Admin123'  --base-url=https://local.domain.com --base-url-secure=https://local.domain.com --backend-frontname=admin --db-host=mysql --db-name=magento --db-user=root --db-password=root  --use-rewrites=1 --language=nl_NL --currency=EUR --timezone=Europe/Amsterdam --use-secure-admin=1 --admin-use-security-key=1 --session-save=files --use-sample-data  

## Set all filepermissions and webserver user group
cd app  
find . -type f -exec chmod 644 {} \;  
find . -type d -exec chmod 755 {} \;  
chmod 644 ./app/etc/*.xml  
chown -R thom:www-data .  
chmod u+x bin/magento  
