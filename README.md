# moodle4-bitnami
Moodle 4.1.4

## Folders required
- 



# For network specific

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
    networks:
      sgevea-docker_sgeveanet:
        ipv4_address: 10.99.0.11

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
    networks:
      sgevea-docker_sgeveanet:
        ipv4_address: 10.99.0.12
networks:
  sgevea-docker_sgeveanet:
    external: true
