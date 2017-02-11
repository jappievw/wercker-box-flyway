# Wercker Box Flyway

This container image is intended to be used as a box for Wercker Pipelines to test and execute database migrations with [Flyway](https://flywaydb.org/). It is based on the [Wercker Box Base](https://github.com/jappievw/wercker-box-base), which provides a bare Debian container with some extra packages.

## Usage

Include the box definition either for all pipelines in the `wercker.yml` as follows:

    box: jappievw/wercker-box-flyway
    
    build:
      services:
        - id: mysql
          tag: 5.7
          env:
            MYSQL_ROOT_PASSWORD: secret
            MYSQL_USER: flyway
            MYSQL_PASSWORD: flyway
            MYSQL_DATABASE: flyway
      steps:
        - script:
            code: |
              flyway -url=jdbc:mysql://$MYSQL_PORT_3306_TCP_ADDR/$MYSQL_ENV_MYSQL_DATABASE -user=$MYSQL_ENV_MYSQL_USER -password=$MYSQL_ENV_MYSQL_PASSWORD migrate
