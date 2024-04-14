FROM schoolofdevops/maven:spring

WORKDIR /app

COPY . .

RUN mvn spring-javaformat:apply && \
mvn package -DskipTests && \
mv target/spring-petclinic-2.3.1.BUILD-SNAPSHOT.jar /run/petclinic.jar

EXPOSE 8080

WORKDIR /run

CMD java -jar petclinic.jar
