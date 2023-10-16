# MOODLE DOCKER
Este archivo es una guia para levantar instancias moodle en Docker

## Moodle con puertos accesible

version: '3.8'

services:
  evea-00:
    image: docker.io/bitnami/moodle:4.1.1
    ports:
      - '${HTTP_PORT}:8080'
      - '${HTTPS_PORT}:8443'
    environment:
      MOODLE_DATABASE_TYPE : "mysqli"
      MOODLE_DATABASE_HOST: "db"
      MOODLE_DATABASE_PORT_NUMBER: "3306"
      MOODLE_DATABASE_USER: "${MYSQL_USER}"
      MOODLE_DATABASE_PASSWORD: "${MYSQL_PASSWORD}"
      MOODLE_DATABASE_NAME: "${MYSQL_DATABASE}"
      ALLOW_EMPTY_PASSWORD: "${ALLOW_EMPTY_PASSWORD:-no}"
      MYSQL_CLIENT_FLAVOR: "mysql"
      MYSQL_CLIENT_DATABASE_HOST: "db"
      MYSQL_CLIENT_DATABASE_PORT_NUMBER: "3306"
      MYSQL_CLIENT_DATABASE_ROOT_USER: "root"
      MYSQL_CLIENT_DATABASE_ROOT_PASSWORD: "ev.00SV03*23-"
      MYSQL_CLIENT_CREATE_DATABASE_NAME: "eveas01"
      MYSQL_CLIENT_CREATE_DATABASE_USER: "eveas01"
      MYSQL_CLIENT_CREATE_DATABASE_PASSWORD: "eveas01"
      BITNAMI_DEBUG: "true"
    volumes:
      - './www:/bitnami/moodle'
      - './data:/bitnami/moodledata'
    networks:
      eveasdp_eveasnet:
        ipv4_address: 10.99.0.70
networks:
  eveasdp_eveasnet:
    external: true

## Moodle con creacion de base de datos integrada

version: '3.8'

services:
  eveaseguimiento:
    image: docker.io/bitnami/moodle:4.1.1
    environment:
      MOODLE_HOST: "seguimiento.unae.edu.ec"
      MOODLE_REVERSEPROXY: "true"
      MOODLE_SSLPROXY: "true"

      MOODLE_USERNAME: "${MOODLE_USERNAME:-admin}"
      MOODLE_PASSWORD: "${MOODLE_PASSWORD:-admin}"
      MOODLE_EMAIL: "${MOODLE_EMAIL:-mail@example.com}"
      MOODLE_SITE_NAME: "${MOODLE_SITE_NAME:-moodle}"
      MOODLE_LANG: "${MOODLE_LANG:-en}"
      MOODLE_SKIP_BOOTSTRAP: "${MOODLE_SKIP_BOOTSTRAP:-no}"

      MOODLE_DATABASE_TYPE : "${MOODLE_DATABASE_TYPE}"
      MOODLE_DATABASE_HOST: "${MOODLE_DATABASE_HOST}"
      MOODLE_DATABASE_PORT_NUMBER: "${MOODLE_DATABASE_PORT_NUMBER}"
      MOODLE_DATABASE_USER: "${MOODLE_DATABASE_USER}"
      MOODLE_DATABASE_PASSWORD: "${MOODLE_DATABASE_PASSWORD}"
      MOODLE_DATABASE_NAME: "${MOODLE_DATABASE_NAME}"

      ALLOW_EMPTY_PASSWORD: "${ALLOW_EMPTY_PASSWORD:-no}"
      
      MYSQL_CLIENT_FLAVOR: "${MYSQL_CLIENT_FLAVOR}"
      MYSQL_CLIENT_DATABASE_HOST: "${MOODLE_DATABASE_HOST}"
      MYSQL_CLIENT_DATABASE_PORT_NUMBER: "${MOODLE_DATABASE_PORT_NUMBER}"
      MYSQL_CLIENT_DATABASE_ROOT_USER: "${MYSQL_CLIENT_DATABASE_ROOT_USER}"
      MYSQL_CLIENT_DATABASE_ROOT_PASSWORD: "${MYSQL_CLIENT_DATABASE_ROOT_PASSWORD}"
      MYSQL_CLIENT_CREATE_DATABASE_NAME: "${MOODLE_DATABASE_NAME}"
      MYSQL_CLIENT_CREATE_DATABASE_USER: "${MOODLE_DATABASE_USER}"
      MYSQL_CLIENT_CREATE_DATABASE_PASSWORD: "${MOODLE_DATABASE_PASSWORD}"
      
      BITNAMI_DEBUG: "true"
    volumes:
      - './www:/bitnami/moodle'
      - './data:/bitnami/moodledata'
    networks:
      eveasdp_eveasnet:
        ipv4_address: 10.99.0.71
networks:
  eveasdp_eveasnet:
    external: true


* .ENV
MOODLE_USERNAME= "admin"
MOODLE_PASSWORD= "admin"
MOODLE_EMAIL= "mail@example.com"
MOODLE_SITE_NAME= "Moodle"
MOODLE_LANG = "es"
MOODLE_SKIP_BOOTSTRAP= "no"
#Do not initialize the Moodle database for a new deployment. This is necessary in case you use a database that already has Moodle data. Default: no

MOODLE_DATABASE_TYPE="mysqli"
MOODLE_DATABASE_HOST="db"
MOODLE_DATABASE_PORT_NUMBER= "3306"
MOODLE_DATABASE_USER= "user"
MOODLE_DATABASE_PASSWORD= "admin"
MOODLE_DATABASE_NAME= "moodle"

#ALLOW_EMPTY_PASSWORD is recommended only for development.
ALLOW_EMPTY_PASSWORD="no"

MYSQL_CLIENT_FLAVOR= "mysql"
MYSQL_CLIENT_DATABASE_ROOT_USER= "root"
MYSQL_CLIENT_DATABASE_ROOT_PASSWORD= "root"

# Moodle con acceso a una base de datos preexistente

version: '3.8'

services:
  eveaseguimiento2:
    image: docker.io/bitnami/moodle:4.1.1
    environment:
      MOODLE_HOST: "example.com"
      MOODLE_REVERSEPROXY: "true"
      MOODLE_SSLPROXY: "true"

      MOODLE_USERNAME: "${MOODLE_USERNAME:-admin}"
      MOODLE_PASSWORD: "${MOODLE_PASSWORD:-admin}"
      MOODLE_EMAIL: "${MOODLE_EMAIL:-mail@example.com}"
      MOODLE_SITE_NAME: "${MOODLE_SITE_NAME:-moodle}"
      MOODLE_LANG: "${MOODLE_LANG:-en}"
      MOODLE_SKIP_BOOTSTRAP: "${MOODLE_SKIP_BOOTSTRAP:-no}"

      MOODLE_DATABASE_TYPE : "${MOODLE_DATABASE_TYPE}"
      MOODLE_DATABASE_HOST: "${MOODLE_DATABASE_HOST}"
      MOODLE_DATABASE_PORT_NUMBER: "${MOODLE_DATABASE_PORT_NUMBER}"
      MOODLE_DATABASE_USER: "${MOODLE_DATABASE_USER}"
      MOODLE_DATABASE_PASSWORD: "${MOODLE_DATABASE_PASSWORD}"
      MOODLE_DATABASE_NAME: "${MOODLE_DATABASE_NAME}"

      ALLOW_EMPTY_PASSWORD: "${ALLOW_EMPTY_PASSWORD:-no}"
           
      BITNAMI_DEBUG: "true"
    volumes:
      - './www:/bitnami/moodle'
      - './data:/bitnami/moodledata'
    networks:
      eveasdp_eveasnet:
        ipv4_address: 10.99.0.72
networks:
  eveasdp_eveasnet:
    external: true


* .env
MOODLE_USERNAME= "admin"
MOODLE_PASSWORD= "admin"
MOODLE_EMAIL= "mail@example.com"
MOODLE_SITE_NAME= "Moodle"
MOODLE_LANG = "es"
MOODLE_SKIP_BOOTSTRAP= "yes"
#Do not initialize the Moodle database for a new deployment. This is necessary in case you use a database that already has Moodle data. Default: no

MOODLE_DATABASE_TYPE="mysqli"
MOODLE_DATABASE_HOST="db"
MOODLE_DATABASE_PORT_NUMBER= "3306"
MOODLE_DATABASE_USER= "root"
MOODLE_DATABASE_PASSWORD= "root"
MOODLE_DATABASE_NAME= "moodle"

#ALLOW_EMPTY_PASSWORD is recommended only for development.
ALLOW_EMPTY_PASSWORD="no"

MYSQL_CLIENT_FLAVOR= "mysql"
MYSQL_CLIENT_DATABASE_ROOT_USER= "root"
MYSQL_CLIENT_DATABASE_ROOT_PASSWORD= "root"

# WITH DATABASE CREATION
version: '3.8'

services:
  mariadb:
    image: docker.io/bitnami/mariadb:11.0
    environment:
      ALLOW_EMPTY_PASSWORD: "${ALLOW_EMPTY_PASSWORD:-yes}"
      MARIADB_USER: "${MARIADB_USER}"
      MARIADB_DATABASE: "${MARIADB_DATABASE}"
      MARIADB_CHARACTER_SET: "utf8mb4"
      MARIADB_COLLATE: "utf8mb4_unicode_ci"
    volumes:
      - './db:/bitnami/mariadb'

  moodle:
    image: docker.io/bitnami/moodle:4.1
    ports:
      - '${HTTP_PORT}:8080'
      - '${HTTPS_PORT}:8443'
    environment:
      MOODLE_DATABASE_HOST: "mariadb"
      MOODLE_DATABASE_PORT_NUMBER: "3306"
      MOODLE_DATABASE_USER: "${MARIADB_USER}"
      MOODLE_DATABASE_NAME: "${MARIADB_DATABASE}"
      ALLOW_EMPTY_PASSWORD: "${ALLOW_EMPTY_PASSWORD:-yes}"
    volumes:
      - './www:/bitnami/moodle'
      - './data:/bitnami/moodledata'
    depends_on:
      - mariadb

* .env
HTTP_PORT="4061"
HTTPS_PORT="4063"


MARIADB_USER="user"
MARIADB_DATABASE="moodle"

#ALLOW_EMPTY_PASSWORD is recommended only for development.
ALLOW_EMPTY_PASSWORD="yes"

## Folders required
- data
- www
- db

chmod 775
chown root:root ./db


# PROXY REVERSE
location / {
    proxy_pass https://eveaseguimiento:8443;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_intercept_errors on;
}
