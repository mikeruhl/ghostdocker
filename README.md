# ghostdocker
Docker Compose file for creating a Ghost Blog all contained within Docker.

## Overview
This repo is for sharing a docker compose file that should be a one-stop shop for setting up a [ghost](https://ghost.org) blog.  It uses a few fantastic containers to automate nearly everything.

### Containers 
Image | Description 
--- | --- 
nginx | will be used as a reverse proxy 
jwilder/docker-gen | Manages nginx based on containers configured.
jrcs/letsencrypt-nginx-proxy-companion | Manages your ssl certificates.
bitnami/mariadb | Our database backend, bitnami flavored.
bitnami/ghost | Our *publishing platform*.  Also bitnami flavored, plays nice with bitnami/mariadb.

## Instructions

I'm assuming you've installed [Docker](https://www.docker.com).

I'm also assuming you've installed [Docker Compose](https://docs.docker.com/compose/install/).

Once those are installed, you can place [docker-compose.yml](https://raw.githubusercontent.com/mikeruhl/ghostdocker/master/docker-compose.yml) in any directory you want.  I usually create directories like ~/blog, ~/registry, etc, etc.

In that SAME directory that you placed the docker-compose file, you'll want to create a file named .env.  For more info on this file, see Docker's excellent [documentation](https://docs.docker.com/compose/environment-variables/).

In that .env file you will place your environmental variables.  These are noted in the docker compose file by being surrounded by curly braces (or squiggly brackets for the technically elite).

Based off that file, you'll add these to your .env file:


```
MARIADB_PASSWORD=[mariadb password]
WEBHOST=[your tld]
MYEMAIL=[your email associated with your certificate]
```

So you'll feed in your mariadb password to both your database and ghost.  When mariadb starts up it will create ad admin password using that.  After your first run, if you persist your data (it's set up that way) then you can remove that line on subsequent runs.

If you travel down to the ghost service, you'll see several environment variables.  These are your URL and ssl variables.  Add VIRTUAL_HOST to any service you want to expose through the reverse proxy and specify a host.  This is defaulted to example.com and www.example.com.
LETSENCRYPT_HOST adds the letsencrypt helper to fetch and maintain the certificate for those domains, so that and VIRTUAL_HOST should match.
LETSENCRYPT_EMAIL sends your email to Lets Encrypt to be associated with that certificate.

### Issues
Submit an issue if you have a question and I will edit this document to provide better clarity.
