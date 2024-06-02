#Build Stage
FROM maven:3.8.7-openjdk-18 as build
WORKDIR /build
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests

#Runtime Stage
FROM amazoncorretto:19

#Define Arguments
ARG APP_VERSION=1.0.0

WORKDIR /app
COPY --from=build /build/target/PatelBros-*.jar /app/

EXPOSE 1323

#Environment Variables
ENV JAR_VERSION=${APP_VERSION}
ENV DB_URL=jdbc:mysql://mysql_ptlbros:3306/patelbros_db?createDatabaseIfNotExist=true
ENV EMAIL_HOSTNAME=missing_host_name
ENV EMAIL_USERNAME=missing_user_name
ENV EMAIL_PASSWORD=missing_password

CMD java -jar -Dspring.datasource.url=${DB_URL} /app/PatelBros-${JAR_VERSION}.jar