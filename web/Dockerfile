FROM webdevops/php-apache:7.4


RUN apt update \
&& mkdir -p /usr/share/man/man1 \
&& apt install -y default-jre \
&& apt install -y default-jdk
RUN apt install nano sed curl

# TODO: test this
RUN adduser thom --disabled-password && usermod -a -G www-data thom

# install executable elasticsearch
RUN cd /home/thom \
&& su -c "wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.12.0-linux-x86_64.tar.gz" thom \
&& su -c "wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.12.0-linux-x86_64.tar.gz.sha512" thom \
&& su -c "shasum -a 512 -c elasticsearch-7.12.0-linux-x86_64.tar.gz.sha512" thom \
&& su -c "tar -xzf elasticsearch-7.12.0-linux-x86_64.tar.gz" thom \
&& sed -i '/cluster\.name/s/^# *//' /home/thom/elasticsearch-7.12.0/config/elasticsearch.yml \
&& sed -i '/node\.name/s/^# *//' /home/thom/elasticsearch-7.12.0/config/elasticsearch.yml \
&& sed -i '/http\.port/s/^# *//' /home/thom/elasticsearch-7.12.0/config/elasticsearch.yml

# TODO: try to run apache2 as thom
