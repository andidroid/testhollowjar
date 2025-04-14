# testhollowjar

mvn clean wildfly-jar:package
mvn clean wildfly-jar:run

mvn wildfly:start
mvn wildfly:shutdown

mvn clean wildfly:package

./target/bootable-jar-build-artifacts/wildfly/bin/standalone.sh
