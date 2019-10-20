# Docker configurations

Dockerfiles for various setups, such as
* nginx for Kohana, Laravel, Symfony, Wordpress
* PHP versions: 5.6, 7.2, 7.3

## Usage

1. Clone the repo into your main project dir:  
    `git clone https://github.com/pronego/docker.git .docker`  
    or as a sub module (in your existing git project):  
    `git submodule add https://github.com/pronego/docker.git .docker`
2. Adjust the *.env* file according to your requirements:
    - Choose the desired framework or system (*kohana*, *laravel*, *symfony*, *wordpress*, *contao*),
    - Specify the PHP version
    - Specify the MySQL version and settings.
3. Change into the .docker dir and run `docker-compose up -d` to start, and 
   `docker-compose down` to stop the containers.


## Useful `docker` commands

To connect a terminal on windows (optionally prepend `winpty` if cmd results in error):  
`docker exec -it <container name> bash`

To rebuild a single container, run:  
`docker-compose up -d --no-deps --build <service_name>`

> `--no-deps` - Don't build linked services from the depends_on section.  
> `--build` - Build images before starting containers.


## Debug settings for PHPStorm
Open `Settings > Language & Frameworks > PHP > Servers` and add a server configuration:\
Usually we use `localhost`, but any name can be used as long as it matches the environment variable setting 
in `docker-compose.yml` (variable in service `php`: `PHP_IDE_CONFIG: "serverName=localhost"`).

- For HTTP debugging with a browser, adjust the path mapping:
  In the same dialog, map project directory to `/var/www/app`.\
  In the debug configuration window, select `Debug as PHP Web Page`.
- For CLI debugging, activate `Listen to PHP Debug Connections` (toolbar, phone button), then open 
  container bash and run app.
  