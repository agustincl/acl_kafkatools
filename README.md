# acl_kafkatools
Ansible for install confluent tools

## Files

- cd /home/ec2-user/security/

- vi __kafka_scram_client_jaas.conf__

```ini
KafkaClient {
org.apache.kafka.common.security.scram.ScramLoginModule required
username="admin"
password="admin-secret";
};
```
  
 - vi __scram_client.properties__

```ini
sasl.mechanism=SCRAM-SHA-256
# Configure SASL_SSL if SSL encryption is enabled, otherwise configure SASL_PLAINTEXT
security.protocol=SASL_SSL
ssl.truststore.location=/var/ssl/private/client.truststore.jks 
ssl.truststore.password=confluenttruststorepass
```
 
 - export KAFKA_OPTS="-Djava.security.auth.login.config=/home/ec2-user/security/kafka_scram_client_jaas.conf"
 - kafka-console-consumer --bootstrap-server ip-10-100-2-224.us-west-2.compute.internal:9092 --topic test_topic --consumer.config /home/ec2-user/security/scram_client.properties --from-beginning
 