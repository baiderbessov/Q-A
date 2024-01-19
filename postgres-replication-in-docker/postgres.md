# Master instance
# docker-compose.yml

version: "3"
services:
  postgresql-master:
    image: *url*/docker-hub/bitnami/postgresql:10.6.0-r1
    restart: always
    network_mode: "host"
    volumes:
      - postgresql_master_data:/bitnami/postgresql
        #  - /data/data-dump/epir_psql_06.01.2024.sql:/docker-entrypoint-initdb.d/db.sql
    environment:
      - POSTGRESQL_PGAUDIT_LOG=READ,WRITE
      - POSTGRESQL_LOG_HOSTNAME=true
      - POSTGRESQL_REPLICATION_MODE=master
      - POSTGRESQL_REPLICATION_USER=repl_user
      - POSTGRESQL_REPLICATION_PASSWORD=repl_user
      - POSTGRESQL_USERNAME=hcms_user
      - POSTGRESQL_PASSWORD=jelathTyadVeugvevSa
      - POSTGRESQL_DATABASE=hcms
      - ALLOW_EMPTY_PASSWORD=yes

volumes:
  postgresql_master_data:
    driver: local


# Slave-1 instance
# docker-compose.yml

version: "3"
services:
  postgresql-slave:
    image: *url*/docker-hub/bitnami/postgresql:10.6.0-r1
    restart: always
    network_mode: "host"
    volumes:
      - postgresql_slave_data:/bitnami/postgresql
    environment:
      - POSTGRESQL_PASSWORD=postgres
      - POSTGRESQL_MASTER_HOST=*master-hostname*
      - POSTGRESQL_PGAUDIT_LOG=READ
      - POSTGRESQL_LOG_HOSTNAME=true
      - POSTGRESQL_REPLICATION_MODE=slave
      - POSTGRESQL_REPLICATION_USER=repl_user
      - POSTGRESQL_REPLICATION_PASSWORD=repl_user
      - POSTGRESQL_MASTER_PORT_NUMBER=5432
      - ALLOW_EMPTY_PASSWORD=yes  
volumes:
  postgresql_slave_data:
    driver: local

# Slave-2 instance
# docker-compose.yml

version: "3"
services:
  postgresql-slave:
    image: *url*/docker-hub/bitnami/postgresql:10.6.0-r1
    restart: always
    network_mode: "host"
    volumes:
      - postgresql_slave_data:/bitnami/postgresql
    environment:
      - POSTGRESQL_PASSWORD=postgres
      - POSTGRESQL_MASTER_HOST=*master-hostname*
      - POSTGRESQL_PGAUDIT_LOG=READ
      - POSTGRESQL_LOG_HOSTNAME=true
      - POSTGRESQL_REPLICATION_MODE=slave
      - POSTGRESQL_REPLICATION_USER=repl_user
      - POSTGRESQL_REPLICATION_PASSWORD=repl_user
      - POSTGRESQL_MASTER_PORT_NUMBER=5432
      - ALLOW_EMPTY_PASSWORD=yes  
volumes:
  postgresql_slave_data:
    driver: local
