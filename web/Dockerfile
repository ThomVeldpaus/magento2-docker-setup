FROM webdevops/php-apache:7.4

RUN apt update \
&& mkdir -p /usr/share/man/man1 \
&& apt install -y nano curl default-jre \
&& apt install -y default-jdk

# RUN curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add - \
# && echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | tee -a /etc/apt/sources.list.d/elastic-7.x.list \
# && apt update \
# && apt install -y elasticsearch

RUN adduser thom --disabled-password && usermod -a -G www-data thom

RUN cd /home/thom \
&& su -c "wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.12.0-linux-x86_64.tar.gz" thom \
&& su -c "wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.12.0-linux-x86_64.tar.gz.sha512" thom \
&& su -c "shasum -a 512 -c elasticsearch-7.12.0-linux-x86_64.tar.gz.sha512" thom \
&& su -c "tar -xzf elasticsearch-7.12.0-linux-x86_64.tar.gz" thom

# RUN cd /home/thom/elasticsearch-7.12.0 \
# && su -c "sed 's/#cluster\.name: my-application/cluster\.name: my-application/' ./config/elasticsearch.yml" \
# && su -c "sed 's/#node\.name: node-1/node\.name: node-1/' ./config/elasticsearch.yml" \
# && su -c "sed 's/#network\.host: 192\.168\.0\.1/network\.host: localhost/' ./config/elasticsearch.yml" \
# && su -c "sed 's/#http\.port: 9200/http\.port: 9200/' ./config/elasticsearch.yml"

