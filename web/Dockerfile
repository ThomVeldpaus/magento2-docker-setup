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

# install Varnish
RUN curl -L https://packagecloud.io/varnishcache/varnish41/gpgkey | apt-key add - \
&& touch  /etc/apt/sources.list.d/varnishcache_varnish41.list \
&& echo "deb https://packagecloud.io/varnishcache/varnish41/ubuntu/ trusty main" >> /etc/apt/sources.list.d/varnishcache_varnish41.list \
&& echo "deb-src https://packagecloud.io/varnishcache/varnish41/ubuntu/ trusty main" >> /etc/apt/sources.list.d/varnishcache_varnish41.list \
&& apt update \
&& apt install -y varnish

RUN sed -i "s/Listen 80/Listen 8080/g" /etc/apache2/ports.conf \
&& sed -i "s/# VARNISH_LISTEN_PORT=6081/VARNISH_LISTEN_PORT=80/g" /etc/default/varnish \
&& cp /etc/varnish/default.vcl /etc/varnish/default.vcl.bak \
# TODO: set hostname in /etc/varnish/default.vcl
&& sed -i 's/.port = "80"/port = "8080"/g' /etc/varnish/default.vcl \
#&& echo "varnishd -d -f /etc/varnish/default.vcl" >> ~/.bashrc \
&& service apache2 restart

