# JasperReports Server CE Edition Docker Container - Minified (alpine version)

The Docker Image aims to quickly get up-and-running a JasperReports Server for a development environment.

This image is build based in [retriever/jasperserver](https://github.com/retrievercommunications/docker-jasperserver) powered by [Nic Grange](mailto:nicolas.grange@retrievercommunications.com).

[![](https://images.microbadger.com/badges/image/pedrorobsonleao/alpine-jasperserver.svg)](https://microbadger.com/images/pedrorobsonleao/alpine-jasperserver "Get your own image badge on microbadger.com") [![](https://images.microbadger.com/badges/version/pedrorobsonleao/alpine-jasperserver.svg)](https://microbadger.com/images/pedrorobsonleao/alpine-jasperserver "Get your own version badge on microbadger.com")
## Start the Container

### Using Command Line

To start the JasperServer container you'll need to pass in 5 environment variables and link it to either a MySQL or Postgres container.

E.g. `docker run -d --name jasperserver -e DB_TYPE=mysql -e DB_HOST=db -e DB_PORT=3306 -e DB_USER=root -e DB_PASSWORD=mysql --link jasperserver_mysql:db -p 8080:8080 retriever/jasperserver`

If you haven't got an existing MySQL or Postgres container then you can easily create one:
`docker run -d --name jasperserver_mysql -e MYSQL_ROOT_PASSWORD=mysql mysql`


### Using Docker-compose

To start up the JasperServer and a MySQL container:

* Run `docker-compose up` to run in foreground or
* Run `docker-compose up -d` to run as in daemon mode.

To stop the containers run `docker-compose stop` and `docker-compose start` to restart them.

Note: To install Docker-compose see the [releases page](https://github.com/docker/compose/releases). 


## Login to JasperReports Web

1. Go to URL http://${dockerHost}:8080/
2. Login using credentials: jasperadmin/jasperadmin


## Image Features
This image includes:
* JasperServer CE Edition version 6.4.0
* IBM DB2 JDBC driver version 4.19.26
* MySQL JDBC driver version 5.1.44
* A volume called '/import' that allows automatic importing of export zip files from another JasperReports Server
* Waits for the database to start before connecting to it using [wait-for-it](https://github.com/vishnubob/wait-for-it) as recommended by [docker-compose documentation](https://docs.docker.com/compose/startup-order/).
* [Web Service Data Source plugin](https://community.jaspersoft.com/project/web-service-data-source) contributed by [@chiavegatto](https://github.com/chiavegatto)

## How to build this image
Use `docker build -t pedrorobsonleao/docker-jasperserver .` 

See comments in Dockerfile to speed up testing by not having to download the jasperserver release each time.

## How to release a new image version
This repo is setup to trigger an automated build of the image [pedrorobsonleao/alpine-jasperserver](https://hub.docker.com/r/pedrorobsonleao/alpine-jasperserver/) on Docker Hub.

To make a new official version of the image, just push a git Tag using the naming convention `major.minor.iteration` where:
* major and minor line up with the included version of jasperserver 
* iteration is incremented each time a change is done that isn't an upgrade of the included jasperserver version
