Management CLI
port 9999

https://james.apache.org/server/manage-cli.html

https://stackoverflow.com/questions/73132367/how-to-config-and-run-apache-james-server-3-7-0-on-windows

james-cli.cmd -h localhost -p 9999 listdomains

WebAdmin cli
https://repo1.maven.org/maven2/org/apache/james/webadmin-cli/3.8.1/
Port 8000

java -jar webadmin-cli-3.8.1.jar domain create mygis.org

java -jar webadmin-cli-3.8.1.jar user create --password=test test@mygis.org
java -jar webadmin-cli-3.8.1.jar user create --password=webgis webgis@mygis.org
java -jar webadmin-cli-3.8.1.jar user create --password=admin admin@mygis.org

Rest API
curl localhost:8000/healthcheck








---

  447  java -jar webadmin-cli-3.8.1.jar
  448  java -jar webadmin-cli-3.8.1.jar --help
  449  java -jar webadmin-cli-3.8.1.jar help
  450  java -jar james-server-cli.jar -h localhost -p 9999 help
  451  java -jar webadmin-cli-3.8.1.jar domain
  452  java -jar webadmin-cli-3.8.1.jar --url=localhost:8000 domain
  453  java -jar webadmin-cli-3.8.1.jar --url=localhost:9999 domain
  454  java -jar webadmin-cli-3.8.1.jar --url=localhost:9999 domainöl
  455  java -jar webadmin-cli-3.8.1.jar --url=localhost:9999999 domain
  456  java -jar webadmin-cli-3.8.1.jar users
  457  java -jar webadmin-cli-3.8.1.jar user
  458  java -jar webadmin-cli-3.8.1.jar user list
  459  java -jar webadmin-cli-3.8.1.jar domain list
  460  java -jar webadmin-cli-3.8.1.jar adddomain mygis.org
  461  java -jar webadmin-cli-3.8.1.jar domain add mygis.org
  462  java -jar webadmin-cli-3.8.1.jar domain mygis.org
  463  java -jar webadmin-cli-3.8.1.jar domain adddomain mygis.org
  464  java -jar webadmin-cli-3.8.1.jar domain addalias mygis.org
  465  java -jar webadmin-cli-3.8.1.jar domain addAlias mygis.org
  466  java -jar webadmin-cli-3.8.1.jar addDomain mygis.org
  467  java -jar webadmin-cli-3.8.1.jar domain help
  468  java -jar webadmin-cli-3.8.1.jar domain --help
  469  java -jar webadmin-cli-3.8.1.jar domain create --help
  470  java -jar webadmin-cli-3.8.1.jar domain create mygis.org
  471  java -jar webadmin-cli-3.8.1.jar domain list
  472  java -jar webadmin-cli-3.8.1.jar user --help
  473  java -jar webadmin-cli-3.8.1.jar user list
  474  java -jar webadmin-cli-3.8.1.jar user create --help
  475  java -jar webadmin-cli-3.8.1.jar user create test@webgis.org --password=test
  476  java -jar webadmin-cli-3.8.1.jar user create --password=test test@webgis.org
  477  java -jar webadmin-cli-3.8.1.jar user create --password=test test@mygis.org
  478  java -jar webadmin-cli-3.8.1.jar user create --password=webgis webgis@mygis.org
  479  java -jar webadmin-cli-3.8.1.jar user create --password=admin admin@mygis.org
  480  java -jar webadmin-cli-3.8.1.jar user create --help
  481  java -jar webadmin-cli-3.8.1.jar domain --help
  482  java -jar webadmin-cli-3.8.1.jar --help
  483  java -jar webadmin-cli-3.8.1.jar help
  484  java -jar webadmin-cli-3.8.1.jar mailbox --help
  485  java -jar webadmin-cli-3.8.1.jar mailbox list
  486  java -jar webadmin-cli-3.8.1.jar mailbox list admin
  487  java -jar webadmin-cli-3.8.1.jar mailbox list admin@mygis.org
  488  java -jar webadmin-cli-3.8.1.jar mailbox create --help
  489  java -jar webadmin-cli-3.8.1.jar mailbox create admin@mygis.org admin-inbox
  490  java -jar webadmin-cli-3.8.1.jar quota list
  491  java -jar webadmin-cli-3.8.1.jar quota
  492  java -jar webadmin-cli-3.8.1.jar quota --help
  493  java -jar webadmin-cli-3.8.1.jar quota global
