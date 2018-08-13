# NAV Kafka Docker Compose
This is a docker-compose project for creating a simple production-alike environment. It can be used for running an application locally, testing kafka adminrest, creating pipelines etc. By default there is no topics created so it might be a good idea to run [kafka-adminrest](https://github.com/navikt/kafka-adminrest/) locally, this will be added to the docker-compose setup later on.

## Technologies used
* docker-compose
* openldap as an replacement for Active Directory
* confluent zookeeper docker image
* confluent kafka docker image with the open source [NAV AD authorization addon](https://github.com/navikt/kafka-plain-saslserver-2-ad)

## Running
Running should be as simple as `docker-compose build`, then `docker-compose up`, the ports for ldap, zookeeper and kafka should be automatically exposed

## Environment variables for kafka-adminrest
These environment variables should work for running kafka-adminrest against docker-compose
```
LDAP_CONNTIMEOUT=2000
LDAP_USERATTRNAME=cn
LDAP_AUTH_HOST=localhost
LDAP_AUTH_PORT=10636
LDAP_SRVUSERBASE=OU=ServiceAccounts,DC=test,DC=local
LDAP_GROUPBASE=OU=kafka,OU=AccountGroupNotInRemedy,OU=Groups,OU=NAV,OU=BusinessUnits,DC=test,DC=local
LDAP_GROUPATTRNAME=cn
LDAP_GRPMEMBERATTRNAME=member
LDAP_USER=igroup
LDAP_PASSWORD=itest
KAFKA_BROKERS=localhost:9092
KAFKA_CLIENTID=kafka-adminrest
KAFKA_SECURITY=TRUE
KAFKA_SECPROT=SASL_PLAINTEXT
KAFKA_SASLMEC=PLAIN
KAFKA_USER=igroup
LDAP_HOST=localhost
LDAP_PORT=10636
LDAP_AUTH_USERBASE=ou=Users,ou=NAV,dc=test,dc=local
KAFKA_PASSWORD=itest
```

## Known issues
See issue tracker on GitHub