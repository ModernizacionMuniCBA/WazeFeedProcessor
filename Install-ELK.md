# Instalacion basica STACK ELK

El procedimiento de instalar y configurar Elasticsearch, Logstash y Kibana en un servidor ubuntu 16.04.5 LTS con paquetes deb descargados e instalados manualmente 

### JAVA 8
Elasticsearch y logstash require que java 8 este instalado. Funciona correrctamente si se quiere instalar con openjdk
```sh
$ add-apt-repository -y ppa:webupd8team/java
$ apt-get update
$ apt-get -y install oracle-java8-installer
```
Funciona correctamente si se quiere instalar con openjdk
### ElasticSearch
**Instalacion**
Descargamos elasticsearch. de la Version 6.3.2 y su sha512
```sh
$ wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.3.2.deb
$ wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.3.2.deb.sha512
```
Comparamos si los  hash son igual.
```sh
$ shasum -a 512 -c elasticsearch-6.3.2.deb.sha512
```
Si es igual procederemos instarlarlo
```sh
$ dpkg -i elasticsearch-6.3.2.deb
```
**Configuracion basica**

 /etc/elasticsearch/elasticsearch.yml
 
 ```sh
 network.host: localhost
 http.port: 9200
 ```
 
 ### Kibana
 
 **Instalacion**
Descargamos kibana Version 6.3.2 y su hash sha-512

```sh
$ wget  https://artifacts.elastic.co/downloads/kibana/kibana-6.3.2-amd64.deb
$ wget  https://artifacts.elastic.co/downloads/kibana/kibana-6.3.2-amd64.deb.sha512
```
Comparamos si los  hash son igual.
```sh
$ shasum -a 512 -c kibana-6.3.2-amd64.deb.sha512
```
Si es igual procederemos instarlarlo
```sh
$ dpkg -i elasticsearch-6.3.2.deb
```
 **Configuracion**
Configuramos que  se puede acceder a kibana solo localamente. Utilizaremos nginx que actuara como reverse proxy(proxy_pass) desde el puerto 80 al puerto 5601
 /etc/kibana/kibana.yml
 ```sh
server.port: 5601
server.host: "localhost"
```

 ### Logstash
**Instalacion**
Descargamos Logstash Version 6.3.2 y su hash sha-512
 ```sh
 wget https://artifacts.elastic.co/downloads/logstash/logstash-6.3.2.deb
 wget https://artifacts.elastic.co/downloads/logstash/logstash-6.3.2.deb.sha512
```
```sh
shasum -a 512 -c logstash-6.3.2.deb.sha512
```
```sh
$ dpkg -i logstash-6.3.2.deb
```

 ### Nginx
 **Instalacion**
 ```sh
 apt-get install nginx apache2-utils
 ```
 **Configuracion**
/etc/nginx/sites-available/default
  ```sh
server {
  listen 80;
  server_name kibana;

  error_log   /var/log/nginx/kibana.error.log;
  access_log  /var/log/nginx/kibana.access.log;

  location / {
    rewrite ^/(.*) /$1 break;
    proxy_ignore_client_abort on;
    proxy_pass http://localhost:5601;

    auth_basic "Restricted Content";
    auth_basic_user_file /etc/nginx/.htpasswd;
    proxy_set_header  X-Real-IP  $remote_addr;
    proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header  Host $http_host;
     }
}
```
Ingresamos usuario kibanadmin
 ```sh
    htpasswd -c /etc/nginx/.htpasswd kibanaadmin
 ```
