# -------------------- STAGE 1 --------------------
  FROM openjdk:17-jdk-slim AS builder
  WORKDIR /app
  RUN apt-get update && apt-get install -y maven
  COPY pom.xml .
  COPY src ./src
  RUN mvn clean package -DskipTests
  
  # -------------------- STAGE 2 --------------------
  FROM openjdk:17-jdk-slim
  WORKDIR /app
  COPY --from=builder /app/target/*.jar app.jar
  EXPOSE 8080
  ENTRYPOINT ["java","-jar","app.jar"]
  

#   #Stage 1 (Builder):
# Uses openjdk:17-jdk-slim as the base to keep consistency.
# Installs Maven to compile the Java code.
# Copies in pom.xml and src to build the .jar.

# Stage 2 (Runtime):
# Again uses openjdk:17-jdk-slim as the base (no Maven or extra tools needed).
# Copies the final .jar from the builder stage.
# Exposes port 8080 and runs the JAR file.