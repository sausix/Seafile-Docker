# Seafile-Docker 12.0 (Compose)

## Status
- No notification sever
- No search engine
- No SeaDoc
- No (other seafile extras I don't know yet)

## docker-compose.yml
I did exclude caddy and internal Let's Encrypt stuff for reasons. 
Some environemnt variables are used multiple times so I used common variables and interpolation. Check all `*.env` files especially the `.env`.

### mariadb
External MariaDB/MySQL can be used too. Seafile dropped support for unix socket connections.  
Latest version seems to work.

### memcached
That's officially recommended.  
Haven't checked if it is being used because there is no config to point the app to this!?

### seafile
The bare main application. Make sure to set the data directory.  
`./seafile-data` is an example but I recommend not to store (big) data within a docker-compose directories. If you like docker volumes unlike me you can use it too of course.


## Revere proxy
Reverse proxies and HTTPS are quite standard today. Almost everyone will or want use HTTPS/TLS encryption and multiple services on a single IP.   
Seafile 12 went to Caddy reverse proxy!? Never heard of it and I will not change all my virtual hosts because of this. 
So this docker-compose is minimal and uses https://github.com/jwilder/docker-letsencrypt-nginx-proxy-companion .
Untested with newer versions. Mine is old. It should work having basic environment variables in your virtual host appliances:
- `VIRTUAL_HOST=${SUBDOMAIN}`
- `LETSENCRYPT_HOST=${SUBDOMAIN}`
- `VIRTUAL_PORT=80`
Tip: Don't expose ports (80 and 443) via docker or it will conflict with the reverse proxy.
Just look at .env and le.env files.


## TODO
Found a newer docker-compose.yml. Check and migrate: https://manual.seafile.com/12.0/docker/ce/seafile-server.yml


## Source
https://github.com/sausix/Seafile-Docker
