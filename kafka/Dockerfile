FROM openjdk:10-jdk
RUN git clone -b update_to_kafka5 'https://github.com/navikt/kafka-plain-saslserver-2-ad.git'
WORKDIR /kafka-plain-saslserver-2-ad
RUN ./gradlew build -x test
RUN ./gradlew shadowJar -x test

FROM confluentinc/cp-kafka:5.0.0
COPY --from=0 /kafka-plain-saslserver-2-ad/build/libs/kafka-plain-saslserver-2-ad-2.0_0.50.jar /usr/share/java/kafka

ENV KAFKA_PROTOCOL_NAME=SASLPLAINTEXT
ENV KAFKA_LISTENER_SECURITY_PROTOCOL_MAP=SASLPLAINTEXT:SASL_PLAINTEXT
ENV KAFKA_LISTENER_NAME_SASLPLAINTEXT_PLAIN_SASL_SERVER_CALLBACK_HANDLER_CLASS=no.nav.common.security.authentication.SimpleLDAPAuthentication
ENV KAFKA_AUTHORIZER_CLASS_NAME=no.nav.common.security.authorization.SimpleLDAPAuthorizer
ENV KAFKA_SUPER_USERS=User:igroup
#ENV KAFKA_SECURITY_INTER_BROKER_PROTOCOL=SASL_PLAINTEXT
ENV KAFKA_INTER_BROKER_LISTENER_NAME=SASLPLAINTEXT
ENV KAFKA_SASL_MECHANISM_INTER_BROKER_PROTOCOL=PLAIN
ENV KAFKA_SASL_ENABLED_MECHANISMS=PLAIN
ENV KAFKA_DEFAULT_REPLICATION_FACTOR=1
ENV KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1
ENV KAFKA_AUTO_CREATE_TOPICS_ENABLE=false

COPY ldapconfig.yaml /etc/kafka
COPY kafka_server_jaas.conf /etc/kafka
ENV KAFKA_OPTS='-Djava.security.auth.login.config=/etc/kafka/kafka_server_jaas.conf'
ENV CLASSPATH="/etc/kafka"
