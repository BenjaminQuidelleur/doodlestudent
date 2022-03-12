FROM maven:3-openjdk-8 AS build

ADD ./lib ./lib
ADD ./haarcascades ./haarcascades
ADD ./pom.xml ./pom.xml
ADD ./src ./src

RUN mvn install:install-file -Dfile=./lib/opencv-3410.jar -DgroupId=org.opencv -DartifactId=opencv -Dversion=3.4.10 -Dpackaging=jar
RUN mvn install
RUN mvn package

FROM ubuntu:latest AS runtime

COPY --from=build ./lib ./lib
COPY --from=build ./target ./target
COPY --from=build ./haarcascades ./haarcascades

RUN apt-get update
RUN apt-get install -yf default-jre
RUN apt-get install -yf libpng16-16
RUN apt-get install -yf libdc1394-22

EXPOSE 8080

CMD ["java", "-Djava.library.path=lib/ubuntuupperthan18", "-jar", "target/fatjar-0.0.1-SNAPSHOT.jar"]
