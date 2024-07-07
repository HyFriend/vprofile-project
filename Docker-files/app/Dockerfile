FROM openjdk:8 AS BUILT_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/HyFriend/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install

FROM tomcat:8-jre11
LABEL "project"="vprofile"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILT_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]