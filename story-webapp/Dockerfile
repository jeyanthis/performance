FROM java:8 

RUN curl http://apache.mesi.com.ar//jmeter/binaries/apache-jmeter-3.0.tgz -o apache-jmeter-3.0.tgz
RUN tar -xzf apache-jmeter-3.0.tgz
ENV JAVA_OPTS "-Xms512m -Xmx512m"

ADD tests tests
VOLUME ["tests"]
WORKDIR tests

ENTRYPOINT ["/apache-jmeter-3.0/bin/jmeter", "-n"]
