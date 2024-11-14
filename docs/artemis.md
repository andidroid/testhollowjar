https://docs.digital.ai/bundle/devops-deploy-version-v.22.2/page/deploy/how-to/artemis-ha-with-udp.html

https://docs.digital.ai/bundle/devops-deploy-version-v.22.2/page/deploy/how-to/configuring-artemis-(jms-2.0)-ha-setup.html

# Tutorials

https://github.com/arunsrajan/tutorial/tree/main/loadbalancing-artemis-mesh
https://www.youtube.com/@configjavatech/videos

# Installation

./bin/artemis.cmd create mybroker
--> user: artemis
--> password: artemis
--> allow-anonymous: Y

ergibt:
./bin/artemis.cmd create mybroker --user artemis --password artemis --allow-anonymous

# Plugins

--Metrics Plugin
Version 2.2.0 # java ee 8
Version 3.0.0 # jakarta ee 10

https://maven.repository.redhat.com/ga/com/redhat/amq-broker/artemis-prometheus-metrics-plugin/
https://maven.repository.redhat.com/ga/com/redhat/amq-broker/artemis-prometheus-metrics-plugin-servlet/

https://maven.repository.redhat.com/ga/com/redhat/amq-broker/redhat-branding/

siehe https://access.redhat.com/documentation/en-us/red_hat_amq/7.4/html/managing_amq_broker/prometheus-plugin-managing
Download https://mvnrepository.com/artifact/org.apache.activemq/artemis-prometheus-metrics-plugin/1.0.0.CR1-redhat-00018
nach mybroker/lib kopieren
Download https://maven.repository.redhat.com/ga/org/apache/activemq/artemis-prometheus-metrics-plugin-servlet/1.0.0.CR1-redhat-00018/artemis-prometheus-metrics-plugin-servlet-1.0.0.CR1-redhat-00018.war
nach mybroker/web kopieren

cd /d/Programmierung/Programme/apache-artemis-2.18.0/mybroker/bin
./artemis.cmd run
