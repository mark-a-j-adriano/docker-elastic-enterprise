# Creating LOCAL DOCKER REGISTRY

https://docs.docker.com/registry/deploying/


# How to:

1. Set DOTENV file. Copy it from example: `cp .env.dist .env`.

2) Make cache directory: `mkdir silverstripe-cache`.

3) Modify host address list by using `hosts` command. Add `127.0.0.1 <SITE_URL>`

   To force your changes to take effect, flush the DNS cache by entering the following command:

   `dscacheutil -flushcache`

4) Run Docker: `docker-compose up -d`

5) SSH into docker container: `docker-compose exec sample-www bash`
