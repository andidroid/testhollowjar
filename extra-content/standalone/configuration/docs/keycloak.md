https://www.mastertheboss.com/keycloak/keycloak-oauth2-example-with-rest-application/

# Authenticate with the Admin Server

./kcadm.sh config credentials --server http://localhost:8180 --realm master --user admin --password admin

# Create Realm testrealm

./kcadm.sh create realms -s realm=testrealm -s enabled=true -o

# Create User testuser

# -s email="joe@gmail.com"

./kcadm.sh create users -r testrealm -s username=testuser -s enabled=true
./kcadm.sh create users -r testrealm -s username=testadmin -s enabled=true

# Set testuser password

./kcadm.sh set-password -r testrealm --username testuser --new-password testuser
./kcadm.sh set-password -r testrealm --username testadmin --new-password testadmin

# Create Client

./kcadm.sh create clients -r testrealm -s clientId=testwar -s bearerOnly="false" -s "redirectUris=[\"http://localhost:8080/*\"]" -s enabled=true -s directAccessGrantsEnabled=true -s clientAuthenticatorType=client-secret -s secret=clientpassword

# Create Role test

./kcadm.sh create roles -r testrealm -s name=test
./kcadm.sh create roles -r testrealm -s name=admin
./kcadm.sh create roles -r testrealm -s name=user

# Assign Role to testuser

./kcadm.sh add-roles --uusername testuser --rolename test -r testrealm
./kcadm.sh add-roles --uusername testuser --rolename user -r testrealm

./kcadm.sh add-roles --uusername testadmin --rolename test -r testrealm
./kcadm.sh add-roles --uusername testadmin --rolename user -r testrealm
./kcadm.sh add-roles --uusername testadmin --rolename admin -r testrealm
