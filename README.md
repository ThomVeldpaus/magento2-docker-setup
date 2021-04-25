# Docker installation Magento 2

## Cheatsheet

### Docker compose build

docker-compose up -d --build 

if you can access 127.0.0.1:8080 you should land on phpmyadmin

### Exec bash in the web service

docker exec -it web bash



### Deploy sampledata

cd ./app

php bin/magento sampledata:deploy

### Install magento (WARNING: WITH SAMPLEDATA!)

php bin/magento setup:install --admin-firstname=Thom --admin-lastname=Veldpaus --admin-email=thom@example.com --admin-user=admin --admin-password='Admin123' --base-url=https://local.domain.com --base-url-secure=https://local.domain.com --backend-frontname=admin --db-host=mysql --db-name=magento --db-user=root --db-password=root --use-rewrites=1 --language=nl_BE --currency=EUR --timezone=Europe/Amsterdam --use-secure-admin=1 --admin-use-security-key=1 --session-save=files --use-sample-data