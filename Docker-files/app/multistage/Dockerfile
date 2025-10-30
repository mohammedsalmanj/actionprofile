# ---------- Build Stage ----------
FROM maven:3.9.9-eclipse-temurin-21-jammy AS build
WORKDIR /app
COPY . .
RUN mvn clean install -DskipTests

# ---------- Runtime Stage ----------
FROM tomcat:10-jdk21
WORKDIR /usr/local/tomcat

# Clean default ROOT app
RUN rm -rf webapps/*

# Copy built WAR from the builder image
COPY --from=build /app/target/vprofile-v2.war webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
