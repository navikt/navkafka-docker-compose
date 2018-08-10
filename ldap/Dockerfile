FROM osixia/openldap:1.2.1

ADD sAMAccountName.schema /container/service/slapd/assets/config/bootstrap/schema/custom/s_ama_account_name.schema
ADD acl.ldif /container/service/slapd/assets/config/bootstrap/ldif/custom/110-acl.ldif
ADD UsersAndGroups.ldif /container/service/slapd/assets/config/bootstrap/ldif/custom/120-users.ldif
ENV LDAP_DOMAIN="test.local"
