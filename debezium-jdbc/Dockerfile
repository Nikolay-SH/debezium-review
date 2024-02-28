ARG DEBEZIUM_VERSION
FROM debezium/connect:${DEBEZIUM_VERSION}
ENV KAFKA_CONNECT_JDBC_DIR=$KAFKA_CONNECT_PLUGINS_DIR/kafka-connect-jdbc

ARG POSTGRES_VERSION=42.2.8
ARG JMX_AGENT_VERSION=0.20.0
ARG KAFKA_JDBC_VERSION=10.7.4

# Deploy PostgreSQL JDBC Driver
RUN cd /kafka/libs && curl -sO https://jdbc.postgresql.org/download/postgresql-$POSTGRES_VERSION.jar

# Deploy Kafka Connect JDBC
RUN mkdir $KAFKA_CONNECT_JDBC_DIR && cd $KAFKA_CONNECT_JDBC_DIR &&\
	curl -sO https://packages.confluent.io/maven/io/confluent/kafka-connect-jdbc/$KAFKA_JDBC_VERSION/kafka-connect-jdbc-$KAFKA_JDBC_VERSION.jar

# Deploy Kafka Connect Prometheus agent
RUN mkdir /kafka/etc && cd /kafka/etc &&\
        curl -so jmx_prometheus_javaagent.jar \
        https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/$JMX_AGENT_VERSION/jmx_prometheus_javaagent-$JMX_AGENT_VERSION.jar

COPY config.yml /kafka/etc/config.yml