FROM tomcat:9 as baseimg

ENV TOMCAT_USERNAME=tomcat
ENV TOMCAT_PASSWORD=tomcat
ENV JAVA_OPTS=-javaagent:/usr/local/tomcat/newrelic/newrelic.jar

RUN mkdir -p /usr/local/tomcat/newrelic/logs
RUN useradd tomcat
RUN chown -R tomcat /usr/local/tomcat/newrelic/logs
ADD ./newrelic.jar /usr/local/tomcat/newrelic/newrelic.jar
ADD ./newrelic.yml /usr/local/tomcat/newrelic/newrelic.yml
# Add the newrelic.jar and -javaagent parameters
RUN mkdir -p /usr/local/tomcat/newrelic
ADD ./newrelic.jar /usr/local/tomcat/newrelic/
ENV JAVA_OPTS="$JAVA_OPTS -javaagent:/usr/local/tomcat/newrelic/newrelic.jar"
# Add the configuration file
ADD ./newrelic/newrelic.yml /usr/local/tomcat/newrelic/
# An example of setting a system property config
ENV JAVA_OPTS="$JAVA_OPTS -Dnewrelic.config.app_name='my-application'"
# An example of setting an Environment variable config
ENV NEW_RELIC_LICENSE_KEY="license_key"
# Config to include the agent logs in Docker's stdout logging
ENV JAVA_OPTS="$JAVA_OPTS -Dnewrelic.config.log_file_name=STDOUT"
ADD ./run.sh /app/run.sh
RUN chmod a+x /app/run.sh
EXPOSE 8089
CMD /app/run.sh
#CMD ["catalina.sh", "run"]

FROM openjdk:8
ADD my-application.jar /app
ADD newrelic.jar  /app
ADD newrelic.yml  /app 
ENV NEW_RELIC_APP_NAME="my-application"
ENV NEW_RELIC_LICENSE_KEY="license_key"
ENV NEW_RELIC_LOG_FILE_NAME="STDOUT"
ENTRYPOINT ["java","-javaagent:/app/newrelic.jar","-jar","/app/my-application.jar"]
