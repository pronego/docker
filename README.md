# Docker configurations

Dockerfiles for various setups, such as
* nginx for Kohana, Laravel, Symfony, Wordpress
* PHP 5.6, PHP 7.2

## Usage

1. Clone the repo into your main project dir:  
    `git clone https://github.com/pronego/docker.git`  
    or as a sub module (in your existing git project):  
    `git submodule add https://github.com/pronego/docker.git`
2. Adjust the *.env* file according to your requirements:
    - Choose the desired framework or system (*kohana*, *laravel*, *symfony*, *wordpress*),
    - Specify the PHP version
    - Specify the MySQL version and settings.
3. Move .env and docker-compose to the top dir
4. Run `docker-compose up -d`