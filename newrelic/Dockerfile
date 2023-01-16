FROM openjdk:8 as baseimg
RUN mkdir -p /app/
ADD ./hello-world-spring-boot/target/myproject-0.0.1-SNAPSHOT.jar /app/my-application.jar
ADD ./hello-world-spring-boot/run.sh /app/run.sh

ENV TOMCAT_USERNAME=tomcat
ENV TOMCAT_PASSWORD=tomcat
ENV JAVA_OPTS=-javaagent:/usr/local/tomcat/newrelic/newrelic.jar

RUN mkdir -p /usr/local/tomcat/newrelic/logs
RUN useradd tomcat
RUN chown -R tomcat /usr/local/tomcat/newrelic/logs
# Add the newrelic.jar and -javaagent parameters
RUN mkdir -p /usr/local/tomcat/newrelic
ADD ./newrelic/newrelic.jar /usr/local/tomcat/newrelic/
ENV JAVA_OPTS="$JAVA_OPTS -javaagent:/usr/local/tomcat/newrelic/newrelic.jar"
# Add the configuration file
ADD ./newrelic/newrelic.yml /usr/local/tomcat/newrelic/
# An example of setting a system property config
ENV JAVA_OPTS="$JAVA_OPTS -Dnewrelic.config.app_name='my_application'"
# An example of setting an Environment variable config
ENV NEW_RELIC_LICENSE_KEY="license_key"
# Config to include the agent logs in Docker's stdout logging
ENV JAVA_OPTS="$JAVA_OPTS -Dnewrelic.config.log_file_name=STDOUT"
#COPY ./hello-world-spring-boot/target/myproject-0.0.1-SNAPSHOT.jar /app/my-application.jar
#COPY ./newrelic/my-application.jar /app/my-application.jar
#COPY ./ ./
ADD newrelic.jar  /app
ADD newrelic.yml  /app 
ENV NEW_RELIC_APP_NAME="my_application"
ENV NEW_RELIC_LICENSE_KEY="license_key"
ENV NEW_RELIC_LOG_FILE_NAME="STDOUT"
EXPOSE 8080:8080
ENTRYPOINT ["java","-javaagent:/app/newrelic.jar","-jar","/app/my-application.jar"]
#ADD ./run.sh /run.sh
#RUN chmod a+x /app/run.sh
#CMD /app/run.sh
