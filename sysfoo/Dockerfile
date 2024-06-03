FROM maven:3.6.1-jdk-7-alpine as build
WORKDIR /opt/demo
COPY . .
RUN mvn package -D skipTests

FROM tomcat as run
WORKDIR /usr/local/tomcat
COPY --from=build /opt/demo/target/sysfoo.war webapps/ROOT.war
CMD catalina.sh run
