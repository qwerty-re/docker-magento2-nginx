# Nginx for Magento 2

[![Nginx version](https://img.shields.io/badge/nginx-1.16.1-green?logo=nginx)](https://nginx.org/en/CHANGES-1.16)
[![Magento nginx config version](https://img.shields.io/badge/nginx.conf-2.3.2-green?logo=magento)](https://github.com/magento/magento2/blob/2.3/nginx.conf.sample)
[![Release](https://img.shields.io/github/v/release/qwerty-re/docker-magento2-nginx)](https://github.com/qwerty-re/docker-magento2-nginx/releases)
[![Docker Hub downloads](https://img.shields.io/docker/pulls/qwertyre/magento2-nginx)](https://hub.docker.com/r/qwertyre/magento2-nginx)
[![Travis](https://img.shields.io/travis/qwerty-re/docker-magento2-nginx)](https://travis-ci.org/qwerty-re/docker-magento2-nginx)
[![License](https://img.shields.io/github/license/qwerty-re/docker-magento2-nginx)](https://github.com/qwerty-re/docker-magento2-nginx/blob/master/LICENSE)

[![Stars](https://img.shields.io/github/stars/qwerty-re/docker-magento2-nginx?style=social)](https://github.com/qwerty-re/docker-magento2-nginx/stargazers)
[![Forks](https://img.shields.io/github/forks/qwerty-re/docker-magento2-nginx?style=social)](https://github.com/qwerty-re/docker-magento2-nginx/network/members)

##### Description

This is simple nginx image for docker with prebuild magento nginx config file.

**Important**

On default configuration php container must by named `DOCKERIZED_MAGENTO2_PHP` ( container_name ).
You can change this value by executing `updateUpstreamBackend` or overriding `default.conf` file.

If you don't check this, nginx container will be exiting with error:

```log
2019/08/29 12:24:12 [emerg] 1#1: host not found in upstream "DOCKERIZED_MAGENTO2_PHP:9000" in /etc/nginx/conf.d/default.conf:2
nginx: [emerg] host not found in upstream "DOCKERIZED_MAGENTO2_PHP:9000" in /etc/nginx/conf.d/default.conf:2
```

##### Example docker-composer configuration
 
 ```yaml
version: '2'
services:
  dockerized_magento2_nginx:
    container_name: DOCKERIZED_MAGENTO2_NGINX
    image: qwertyre/magento2-nginx:1.16.1
    volumes:
      - ./local-magento:/srv/magento2
    network_mode: "DOCKER_network"
    depends_on:
      - magento2_raw_php
```

##### Changing upstream backend host
 
 ```shell script
export PHP_BACKEND=MAGENTO2_php
/usr/loca/bin/updateUpstreamBackend
```
 
 ##### Overriding example for default.conf
 
Click here to download file for overriding [default.conf](https://github.com/qwerty-re/docker-magento2-nginx/blob/master/container/etc/nginx/conf.d/default.conf)
 
 ```yaml
version: '2'
services:
  dockerized_magento2_nginx:
    container_name: DOCKERIZED_MAGENTO2_NGINX
    image: qwertyre/magento2-nginx:1.16.1
    volumes:
      - ./magento-2.3.1:/srv/magento2
      - ./mount/nginx/custom.conf:/etc/nginx/conf.d/default.conf
    ...
```


