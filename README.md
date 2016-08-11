# xibo-docker
CMS 소스는 
https://github.com/gractor/xibo-cms
여기 기준으로 설치됩니다


Docker container for the Xibo Digital Signage CMS

Docker Hub repository: https://hub.docker.com/r/chimeradev/xibo-docker/

# Environment variables

Pass these environment variables when running the container to modify settings:

Variable Name | Description | Default Value
--------------|-------------|--------------
MYSQL_HOST    | The MySQL Hostname/IP | localhost
MYSQL_PASS    | A MySQL user "admin" will be created, this is his password | changeme
XIBO_ADMIN_PASS | A Xibo user "admin" will be created, this is his password | changeme
MYSQL_DBNAME | The name of the database which should be created for Xibo | xibo

# build 

 sudo docker build -t gractor/xibo .

# Running the container

`docker run -p 80:80 -e XIBO_ADMIN_PASS=secret -e MYSQL_PASS=topsecret gractor/xibo`

# Data Container

It's a best practice to have data separated from the actual server container. Our Xibo image stores its data in the folder /xibo-data/, which can be mapped into a data container:

`docker create -v /xibo-data --name xibo-data chimeradev/xibo /bin/true && 
docker run -d --volumes-from xibo-data --name xibo -p 80:80 -e XIBO_ADMIN_PASS=secret -e MYSQL_PASS=topsecret chimeradev/xibo`
