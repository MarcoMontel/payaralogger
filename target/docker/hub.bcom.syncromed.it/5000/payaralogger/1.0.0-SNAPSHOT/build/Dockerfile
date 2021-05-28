# Copyright (C) 2019 - 2019 FUJIFILM Italia S.p.A.
# Medical Informatics Research & Development Unit
# All Rights Reserved

FROM payara/micro:5.2021.3

USER root

ADD ["target/payaralogger.war",  "$DEPLOY_DIR/"]

ENTRYPOINT [ "sh", "-c", "java -jar /opt/payara/payara-micro.jar \
                               --postbootcommandfile /resources/postBoot \
                               --deploymentDir $DEPLOY_DIR \
                               --logToFile /var/log/payara/server.log"]
