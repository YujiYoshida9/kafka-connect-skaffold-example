# Kafka Connect skaffold Example

## Retrieve Kafka

To retrieve Kafka, use the following command:


helm pull oci://registry-1.docker.io/bitnamicharts/kafka
After downloading, extract the files using:
tar -xvzf <downloaded_file_name>.tgz
Replace <downloaded_file_name> with the actual name of the downloaded file.


In this example, the Kafka protocol is set to plaintext. Please make sure to change this setting for production use.



# debezium/connect pod

## Generate Kafka Connect Connector

To generate a Kafka Connect connector, use the following `curl` command. This command creates a connector using the Kafka Connect REST API.

```bash
curl -X POST -H "Content-Type: application/json" --data '{
  "name": "inventory-connector",
  "config": {
    "connector.class": "io.debezium.connector.postgresql.PostgresConnector",
    "tasks.max": "1",
    "database.hostname": "debezium-postgres",
    "database.port": "5432",
    "database.user": "postgres",
    "database.password": "password",
    "database.dbname": "postgresdb",
    "database.server.name": "dbserver1",
    "table.include.list": "public.inventory",
    "topic.prefix": "dbserver1"
  }
}' http://localhost:8083/connectors

## Run Skaffold

To run `skaffold dev -p dev`, use the following command:
