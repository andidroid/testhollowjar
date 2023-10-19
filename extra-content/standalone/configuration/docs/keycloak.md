https://www.mastertheboss.com/keycloak/keycloak-oauth2-example-with-rest-application/

## Authenticate with the Admin Server

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

./kcadm.sh create clients -r testrealm -s clientId=testwar -s bearerOnly="false" -s "redirectUris=[\"http://localhost:8080/*\,\"https://localhost:8443/*\"]" -s enabled=true -s directAccessGrantsEnabled=true -s clientAuthenticatorType=client-secret -s secret=clientpassword

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
