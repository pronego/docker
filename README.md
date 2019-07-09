# Docker configurations

Dockerfiles for various setups, such as
* nginx for Kohana, Laravel, Symfony, Wordpress
* PHP 5.6, PHP 7.2

## Usage

1. Clone the repo into your main project dir:  
    `git clone https://github.com/pronego/docker.git .docker`  
    or as a sub module (in your existing git project):  
    `git submodule add https://github.com/pronego/docker.git .docker`
2. Adjust the *.env* file according to your requirements:
    - Choose the desired framework or system (*kohana*, *laravel*, *symfony*, *wordpress*),
    - Specify the PHP version
    - Specify the MySQL version and settings.
3. Change into the .docker dir and run `docker-compose up -d`

## Useful `docker` commands

To connect a terminal on windows (optionally prepend `winpty` if cmd results in error:  
`docker exec -it <container name> bash`

To rebuild a single container, run:  
`docker-compose up -d --no-deps --build <service_name>`

> `-no-deps` - Don't start linked services.  
> `--build` - Build images before starting containers.