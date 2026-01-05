FROM eclipse-temurin:8-jdk-alpine

# ---- Environment ----
ENV JAVA_HOME=/opt/java/openjdk \
    PATH=$PATH:/opt/java/openjdk/bin \
    APP_HOME=/app/bin \
    OTEL_AGENT_VERSION=1.32.0 \
    OTEL_AGENT_JAR_FILE=opentelemetry-javaagent.jar \
    MIN_HEAP_SIZE=40M \
    MAX_HEAP_SIZE=512M \
    THREADSTACK_SIZE=228k \
    JAVA_GC_ARGS="-XX:MinHeapFreeRatio=20 -XX:MaxHeapFreeRatio=40 -XX:+UseSerialGC -XX:GCTimeRatio=4 -XX:AdaptiveSizePolicyWeight=90" \
    JAVA_OPTS="-server -Duser.timezone=America/Chicago -Djava.security.egd=file:/dev/./urandom -XX:CompressedClassSpaceSize=64m -XX:MaxMetaspaceSize=256m" \
    JAVA_DIAG_ARGS="" \
    JAVA_OPTS_APPEND=""

# ---- Create app directory ----
RUN mkdir -p ${APP_HOME}

# ---- Copy startup script ----
COPY scripts/start-app.sh ${APP_HOME}/start-app.sh

# ---- Download OpenTelemetry Java Agent ----
ADD https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v${OTEL_AGENT_VERSION}/${OTEL_AGENT_JAR_FILE} \
    ${APP_HOME}/${OTEL_AGENT_JAR_FILE}

# ---- Permissions ----
RUN chmod +x ${APP_HOME}/start-app.sh

WORKDIR ${APP_HOME}

CMD ["sh", "/app/bin/start-app.sh"]
