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

