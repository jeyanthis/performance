FROM java:8-jre-alpine

RUN apk add --update curl && \
    rm -rf /var/cache/apk/*

RUN curl http://apache.mesi.com.ar//jmeter/binaries/apache-jmeter-3.0.tgz -o apache-jmeter-3.0.tgz
RUN tar -xzf apache-jmeter-3.0.tgz
ENV JAVA_OPTS "-Xms512m -Xmx512m"

RUN mkdir /results
COPY tests /tests

ENTRYPOINT ["/apache-jmeter-3.0/bin/jmeter", "-n"]
