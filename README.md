Synapp V1 HTTPS LAMP docker-compose definition
==============================================
####*HTTPS LAMP stack on docker containers*

 Copyright (C) 2012-2019 Gael Abadin  
 License: [MIT Expat][1]
<br/>

## About this repo

The main purpose of this project is to simplify the single server deployment migration of an HTTPS LAMP stack by leveraging docker container official images. 

This repo contains a basic docker compose definition and resources for deploying a basic LAMP (Linux, Apache MariaDB, PHP) stack on docker containers. It is used on synapp's project deployments, including production environments.

I've tried this stuff on CentOS 7 and Debian 9 AWS EC2 AMIs. So far no issues.


## Usage

First you need to set up a host machine with docker and docker compose (go to https://docs.docker.com/get-started/ to figure out how). After that, complete these actions:

 * (optional) Build a customized docker image from the latest official `php-fpm` image to enable the desired php extensions (`docker build -t redux-php-fpm:latest redux-php-fpm`)
 * Ensure your `/var/lib/mysql` files are present on `db-data` folder. If you leave the folder empty, the volume will be populated with a freshly initialized maridb deployment so you can also manually run your app's DDL and db init scripts.
 * Ensure your application folder (e.g. `/synapp`) is present on `www-data` folder, build and configured as described on [the app's main repo][4].
 * Ensure your server public certificate, private key, and ca-bundle are present on `redux-httpd/certificates` folder
 * Make sure `/redux-mariadb/mariadb.env` is created and populated with the env vars defined on `/redux-mariadb/mariadb.env.template`
 * Make sure `/redux-httpd/httpd.env` is created and populated with the env vars defined on `/redux-httpd/httpd.env.template`

When all of the above is done, deploy using `docker-compose up`.


## Change Log

 * See [CHANGELOG.md](CHANGELOG.md)

## Known Issues

 * `mariadb` docker image is known not to work well with data on docker volumes on windows. Use a linux VM docker host instead.

## Requirements and dependencies

 * Docker and docker-compose version 2 or greater


## TODO

* Use this project as a base project for cloud build and deploy a fresh app directly from the repo's latest final release


## About synapp project

This project was completed on 2012 during an Erasmus internship on [Akademia 
Gorniczo-Hutnicza University of Science an Technology][23] (Krakow), under the 
supervision of [Professor Bipin Indurkhya][2] at [AGH-UST's Computer Science 
Department][24] and [Professor Juan Carlos Burguillo Rial][3] at the 
[Telematics Engineering Department][25] of [Universidade de Vigo][26].

Its purpose is to present an experiment consisting on a series of 
crowd-sourcing related activities through an online web platform for exploring 
and developing its user's cognitive skills related with the creative process.

More info on [Synapp project's main repo][4]


## License

This code and the libraries it depends on (3rd party and own) have 
[GPLv2][16] compatible licenses that allow commercial and non commercial use 
free of charge. Check out the [LICENSE][1] file for more specific information 
on the MIT Expat license, used on all code and resources published on synapp's 
main public repository. Check out each dependency repository for specific info 
on its GPLv2 compatible license, which should be found on the LICENSE file of 
its root folder.

[1]: https://bitbucket.org/synappv1/synapp/raw/master/LICENSE
[2]: http://www.ki.agh.edu.pl/en/staff/indurkhya-bipin
[3]: https://sites.google.com/site/jcburgui/
[4]: https://github.com/elcodedocle/synapp
[16]: http://www.gnu.org/licenses/gpl-2.0.html
[23]: http://www.agh.edu.pl/en/
[24]: http://www.ki.agh.edu.pl/en
[25]: http://www-gist.det.uvigo.es
[26]: http://uvigo.es
