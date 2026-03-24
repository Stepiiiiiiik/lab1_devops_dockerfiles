# not use multi stage build
FROM gradle:8.11.1-jdk23 AS builder

RUN groupadd -r hello && useradd --no-log-init -r -g hello hello

WORKDIR /app

COPY . .

RUN gradle jar --no-daemon

FROM eclipse-temurin:23-jre-alpine

WORKDIR /app

COPY --from=builder /app/build/libs/*.jar app.jar

ENTRYPOINT ["java"]
CMD ["-jar", "/app/app.jar"]
