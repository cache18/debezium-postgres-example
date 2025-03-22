# debezium-postgres-example
easy example how to set up debezium with postgresql and kafka using docker


1) docker-compose up -d

2) register debezium connector:</br>
   curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @register-postgres.json

3) create kafka topic:</br>
   ./opt/bitnami/kafka/bin/kafka-console-consumer.sh --bootstrap-server kafka:9092 --from-beginning --property print.key=true --topic dbserver1.inventory.customers

4) create schema(inventory) and table(customers) in db:</br>
<code></br>
CREATE TABLE customers(</br>
    id SERIAL,</br>
    first_name VARCHAR(255) NOT NULL,</br>
    last_name VARCHAR(255) NOT NULL,</br>
    email VARCHAR(255) NOT NULL,</br>
    PRIMARY KEY(id)</br>
)
</code>

5) add new record in db and check if changes in db are sent to kafka topic</br>
   insert into customers values(1, 'MyName', 'MyLastName', 'email@test.pl');