FROM java:8-jre-alpine

RUN apk add --update curl && \
    rm -rf /var/cache/apk/*

RUN curl https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-3.1.tgz -o apache-jmeter-3.1.tgz
RUN tar -xzf apache-jmeter-3.1.tgz
ENV JAVA_OPTS "-Xms512m -Xmx512m"

RUN mkdir /results
COPY tests /tests

ENTRYPOINT ["/apache-jmeter-3.1/bin/jmeter", "-n"]
