# https://www.mastertheboss.com/keycloak/keycloak-oauth2-example-with-rest-application/

# https://www.keycloak.org/docs/latest/server_admin/index.html#admin-cli

## Authenticate with the Admin Server

# zuerst http://localhost:9180 öffnen und admin user mit admin passwort anlegen, danach lokal authentifizieren

./kcadm.sh config credentials --server http://localhost:9180 --realm master --user admin --password admin

## Create Realm testrealm

./kcadm.sh create realms -s realm=testrealm -s enabled=true -o

## Create User testuser

## -s email="joe@gmail.com"

./kcadm.sh create users -r testrealm -s username=testuser -s enabled=true
./kcadm.sh create users -r testrealm -s username=testadmin -s enabled=true

## Set testuser password

./kcadm.sh set-password -r testrealm --username testuser --new-password testuser
./kcadm.sh set-password -r testrealm --username testadmin --new-password testadmin

## Create Client

# TODO redirect url with \" on windows bat script "redirectUris=[\"http://localhost:8080/*\,\"https://localhost:8443/*\"]"

./kcadm.sh create clients -r testrealm -s clientId=testwar -s bearerOnly="false" -s "redirectUris=[\"http://localhost:8080/*\",\"https://localhost:8443/*\"]" -s enabled=true -s directAccessGrantsEnabled=true -s clientAuthenticatorType=client-secret -s secret=clientpassword

## Create Role test

./kcadm.sh create roles -r testrealm -s name=test
./kcadm.sh create roles -r testrealm -s name=admin
./kcadm.sh create roles -r testrealm -s name=user

## Assign Role to testuser

./kcadm.sh add-roles --uusername testuser --rolename test -r testrealm
./kcadm.sh add-roles --uusername testuser --rolename user -r testrealm

./kcadm.sh add-roles --uusername testadmin --rolename test -r testrealm
./kcadm.sh add-roles --uusername testadmin --rolename user -r testrealm
./kcadm.sh add-roles --uusername testadmin --rolename admin -r testrealm

# Artemis Realm

./kcadm.sh create realms -s realm=artemisrealm -s enabled=true -o

./kcadm.sh create users -r artemisrealm -s username=admin -s enabled=true
./kcadm.sh create users -r artemisrealm -s username=artemis -s enabled=true
./kcadm.sh create users -r artemisrealm -s username=viewer -s enabled=true

./kcadm.sh set-password -r artemisrealm --username admin --new-password admin
./kcadm.sh set-password -r artemisrealm --username artemis --new-password artemis
./kcadm.sh set-password -r artemisrealm --username viewer --new-password viewer

### client for Hawtio Console

./kcadm.sh create clients -r artemisrealm -s clientId=artemisconsole -s bearerOnly="false" -s "redirectUris=[\"http://localhost:8161/console/*\",\"https://localhost:8163/console/*\"]" -s enabled=true -s directAccessGrantsEnabled=false -s clientAuthenticatorType=client-secret -s secret=clientpassword -s publicClient="true"

### client for Hawtio Console

./kcadm.sh create roles -r artemisrealm -s name=amq
./kcadm.sh create roles -r artemisrealm -s name=admin
./kcadm.sh create roles -r artemisrealm -s name=guest
./kcadm.sh create roles -r artemisrealm -s name=view
./kcadm.sh create roles -r artemisrealm -s name=update

## Assign Role to testuser

./kcadm.sh add-roles --uusername admin --rolename admin -r artemisrealm
./kcadm.sh add-roles --uusername admin --rolename amq -r artemisrealm
./kcadm.sh add-roles --uusername artemis --rolename amq -r artemisrealm
./kcadm.sh add-roles --uusername viewer --rolename view -r artemisrealm

# Wildfly Admin Console HAL

./kcadm.sh create realms -s realm=wildfly-infra -s enabled=true -o

./kcadm.sh create clients -r wildfly-infra -s clientId=wildfly-console -s bearerOnly="false" -s "redirectUris=[\"http://localhost:9990/console/*\",\"https://localhost:9993/console/*\"]" -s enabled=true -s directAccessGrantsEnabled=true -s clientAuthenticatorType=client-secret -s secret=clientpassword

./kcadm.sh create clients -r wildfly-infra -s clientId=wildfly-management -s bearerOnly="true" -s enabled=true -s directAccessGrantsEnabled=false -s clientAuthenticatorType=client-secret -s secret=clientpassword

./kcadm.sh create roles -r wildfly-infra -s name=Administrator
./kcadm.sh create roles -r wildfly-infra -s name=SuperUser

./kcadm.sh create users -r wildfly-infra -s username=admin -s enabled=true
./kcadm.sh set-password -r wildfly-infra --username admin --new-password admin

./kcadm.sh add-roles --uusername admin --rolename Administrator -r wildfly-infra
./kcadm.sh add-roles --uusername admin --rolename SuperUser -r wildfly-infra

# Application Realm WebGISRealm

./kcadm.sh create realms -s realm=webgisrealm -s enabled=true -o

./kcadm.sh create users -r webgisrealm -s username=test -s enabled=true
./kcadm.sh set-password -r webgisrealm --username test --new-password test

./kcadm.sh create clients -r webgisrealm -s clientId=webgisclient -s bearerOnly="true" -s enabled=true -s directAccessGrantsEnabled=false -s clientAuthenticatorType=client-secret -s secret=clientpassword

# kerberos

./kcadm.sh create components -r webgisrealm -s parentId=4fe9e1b9-5cca-4af9-9230-e09625bb5412 -s name=kerberos-provider -s providerId=kerberos -s providerType=org.keycloak.storage.UserStorageProvider -s 'config.priority=["0"]' -s 'config.debug=["false"]' -s 'config.allowPasswordAuthentication=["true"]' -s 'config.editMode=["UNSYNCED"]' -s 'config.updateProfileFirstLogin=["true"]' -s 'config.allowKerberosAuthentication=["true"]' -s 'config.kerberosRealm=["KEYCLOAK.ORG"]' -s 'config.keyTab=["http.keytab"]' -s 'config.serverPrincipal=["HTTP/localhost@KEYCLOAK.ORG"]' -s 'config.cachePolicy=["DEFAULT"]'

# parentId ist id von webgisrealm (siehe create realsm command) -> id kann mit -s id=realmid auch angegeben werden

./kcadm.sh create components -r webgisrealm -s name=kerberos-ldap-provider -s providerId=ldap -s providerType=org.keycloak.storage.UserStorageProvider -s parentId=4fe9e1b9-5cca-4af9-9230-e09625bb5412 -s 'config.priority=["1"]' -s 'config.fullSyncPeriod=["-1"]' -s 'config.changedSyncPeriod=["-1"]' -s 'config.cachePolicy=["DEFAULT"]' -s config.evictionDay=[] -s config.evictionHour=[] -s config.evictionMinute=[] -s config.maxLifespan=[] -s 'config.batchSizeForSync=["1000"]' -s 'config.editMode=["WRITABLE"]' -s 'config.syncRegistrations=["false"]' -s 'config.vendor=["other"]' -s 'config.usernameLDAPAttribute=["uid"]' -s 'config.rdnLDAPAttribute=["uid"]' -s 'config.uuidLDAPAttribute=["entryUUID"]' -s 'config.userObjectClasses=["inetOrgPerson, organizationalPerson"]' -s 'config.connectionUrl=["ldap://localhost:10389"]' -s 'config.usersDn=["ou=users,dc=webgis,dc=org"]' -s 'config.authType=["simple"]' -s 'config.bindDn=["uid=admin,ou=system"]' -s 'config.bindCredential=["secret"]' -s 'config.searchScope=["1"]' -s 'config.useTruststoreSpi=["always"]' -s 'config.connectionPooling=["true"]' -s 'config.pagination=["true"]' -s 'config.allowKerberosAuthentication=["true"]' -s 'config.serverPrincipal=["HTTP/localhost@KEYCLOAK.ORG"]' -s 'config.keyTab=["http.keytab"]' -s 'config.kerberosRealm=["KEYCLOAK.ORG"]' -s 'config.debug=["true"]' -s 'config.useKerberosForPasswordAuthentication=["true"]'

./kcadm.sh create components -r webgisrealm -s name=kerberos-ldap-provider-2 -s providerId=ldap -s providerType=org.keycloak.storage.UserStorageProvider -s parentId=4fe9e1b9-5cca-4af9-9230-e09625bb5412 -s 'config.priority=["2"]' -s 'config.fullSyncPeriod=["-1"]' -s 'config.changedSyncPeriod=["-1"]' -s 'config.cachePolicy=["DEFAULT"]' -s config.evictionDay=[] -s config.evictionHour=[] -s config.evictionMinute=[] -s config.maxLifespan=[] -s 'config.batchSizeForSync=["1000"]' -s 'config.editMode=["WRITABLE"]' -s 'config.syncRegistrations=["false"]' -s 'config.vendor=["other"]' -s 'config.usernameLDAPAttribute=["uid"]' -s 'config.rdnLDAPAttribute=["uid"]' -s 'config.uuidLDAPAttribute=["entryUUID"]' -s 'config.userObjectClasses=["inetOrgPerson, organizationalPerson"]' -s 'config.connectionUrl=["ldap://localhost:10389"]' -s 'config.usersDn=["ou=users,dc=example,dc=com"]' -s 'config.authType=["simple"]' -s 'config.bindDn=["uid=admin,ou=system"]' -s 'config.bindCredential=["secret"]' -s 'config.searchScope=["1"]' -s 'config.useTruststoreSpi=["always"]' -s 'config.connectionPooling=["true"]' -s 'config.pagination=["true"]' -s 'config.allowKerberosAuthentication=["true"]' -s 'config.serverPrincipal=["HTTP/localhost@KEYCLOAK.ORG"]' -s 'config.keyTab=["http.keytab"]' -s 'config.kerberosRealm=["KEYCLOAK.ORG"]' -s 'config.debug=["true"]' -s 'config.useKerberosForPasswordAuthentication=["true"]'

# trigger user synchronisatin

kcadm.sh create user-storage/b7c63d02-b62a-4fc1-977c-947d6a09e1ea/sync?action=triggerFullSync

# adding group mapper



$ kcadm.sh create components -r webgisrealm -s name=group-ldap-mapper -s providerId=group-ldap-mapper -s providerType=org.keycloak.storage.ldap.mappers.LDAPStorageMapper -s parentId=4fe9e1b9-5cca-4af9-9230-e09625bb5412 -s 'config."groups.dn"=[]' -s 'config."group.name.ldap.attribute"=["cn"]' -s 'config."group.object.classes"=["groupOfNames"]' -s 'config."preserve.group.inheritance"=["true"]' -s 'config."membership.ldap.attribute"=["member"]' -s 'config."membership.attribute.type"=["DN"]' -s 'config."groups.ldap.filter"=[]' -s 'config.mode=["LDAP_ONLY"]' -s 'config."user.roles.retrieve.strategy"=["LOAD_GROUPS_BY_MEMBER_ATTRIBUTE"]' -s 'config."mapped.group.attributes"=["admins-group"]' -s 'config."drop.non.existing.groups.during.sync"=["false"]' -s 'config.roles=["admins"]' -s 'config.groups=["admins-group"]' -s 'config.group=[]' -s 'config.preserve=["true"]' -s 'config.membership=["member"]'

