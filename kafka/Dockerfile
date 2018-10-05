FROM openjdk:10-jdk
RUN git clone 'https://github.com/navikt/kafka-plain-saslserver-2-ad.git'
WORKDIR /kafka-plain-saslserver-2-ad
RUN ./gradlew build -x test
RUN ./gradlew shadowJar -x test

FROM confluentinc/cp-kafka:5.0.0
COPY --from=0 /kafka-plain-saslserver-2-ad/build/libs/kafka-plain-saslserver-2-ad-* /usr/share/java/kafka

COPY ldapconfig.yaml /etc/kafka
COPY kafka_server_jaas.conf /etc/kafka
ENV KAFKA_OPTS='-Djava.security.auth.login.config=/etc/kafka/kafka_server_jaas.conf'
ENV CLASSPATH="/etc/kafka"
