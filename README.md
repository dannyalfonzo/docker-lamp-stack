# docker-lamp-stack
just a lightweight lamp stack (linux - apache - mysql5.7 - php7.1) with docker

### Usage
Make sure that: 
- docker and docker-compose are installed
- you cloned this repository into your favorite directory
- no service is currently running on port 80 or 443

Then just start the docker containers using
```
docker-compose up
```
Now you can connect to your webserver on http://localhost/ or https://localhost/ (with a non trusted certificate)

To stop the current container use
```
docker-compose down
```

### Configuration
##### New vhosts
To enable new vhosts:
- add a new configuration file like `sites-enabled/{{your-new-vhost}}.conf`
- create the directories `sites/{{your-new-vhost}}/html` and `sites/{{your-new-vhost}}/log`
- adding the new domain to your local `/etc/hosts` file like `127.0.0.1 {{your-new-vhost}}`
Afterwards just execute:
```
docker-compose -it lamp_apache_php /etc/init.d/apache2 reload
```
To see an example just have a look on [sites-enabled/test.localhost.conf](./sites-enabled/test.localhost.conf) 
##### Other php version
- make sure the containers are stopped
- change the first line in [php/Dockerfile](./php/Dockerfile) from "FROM php:7.1-apache" to "FROM php:5.6-apache" or another php version (available versions: https://github.com/docker-library/php)
- build the new containers
```
docker-compose build
``` 
- start your lamp stack with the new php version
```
docker-compose up
```
##### Adding php modules
- make sure the containers are stopped
- Open [php/Dockerfile](./php/Dockerfile) and add your lines of code to add a new module (For example there is imagick commented out)
- To enable some modules see https://gist.github.com/tristanlins/4c1da2508f0326a042aa
- Afterwards build the new containers:
```
docker-compose build
``` 

/*********** ADDED BY DANNY *******************/

docker-compose ps<br />

   Name                  Command               State                    Ports                  
-----------------------------------------------------------------------------------------------
lamp_apache   docker-php-entrypoint apac ...   Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
lamp_db       docker-entrypoint.sh mysqld      Up      0.0.0.0:3306->3306/tcp, 33060/tcp

Execute mysql command from the host to container running mysql server<br />
docker exec -t -i lamp_db /bin/bash
root@141f63a75843:/#



