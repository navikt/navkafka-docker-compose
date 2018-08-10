FROM confluentinc/cp-zookeeper:4.0.2

COPY zookeeper_server_jaas.conf /etc/kafka

ENV KAFKA_OPTS='-Djava.security.auth.login.config=/etc/kafka/zookeeper_server_jaas.conf'
