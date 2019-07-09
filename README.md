# Docker configurations

Dockerfiles for various setups, such as
* nginx for Kohana, Laravel, Symfony, Wordpress
* PHP 5.6, PHP 7.2

## Usage

1. Clone the repo: `git clone https://github.com/pronego/docker.git`
2. Adjust the *.env* file according to your requirements:
    - Choose the desired framework or system (*kohana*, *laravel*, *symfony*, *wordpress*),
    - Specify the PHP version
    - Specify the MySQL version and settings.
2. Run `docker-compose up -d`