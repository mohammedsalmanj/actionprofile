# ---------- Build Stage ----------
FROM maven:3.9.9-eclipse-temurin-21-jammy AS build
COPY . /app
WORKDIR /app
RUN mvn clean install -DskipTests

# ---------- Runtime Stage ----------
FROM tomcat:10-jdk21

# Clean default ROOT app
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy built WAR from the builder image
COPY --from=BUILD_IMAGE /app/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
