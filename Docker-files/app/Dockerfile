# Stage 1: Build
FROM openjdk:8 AS BUILT_IMAGE
RUN apt-get update && apt-get install -y maven git
RUN git clone https://github.com/HyFriend/vprofile-project.git
WORKDIR vprofile-project
RUN git checkout docker && mvn install

# Stage 2: Deployment
FROM tomcat:8-jre11
LABEL "project"="vprofile"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILT_IMAGE /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
