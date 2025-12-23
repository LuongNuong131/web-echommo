# 1. Giai đoạn Build: Dùng Maven để tạo file .jar
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
# Build bỏ qua test để tiết kiệm thời gian
RUN mvn clean package -DskipTests

# 2. Giai đoạn Run: Dùng Java siêu nhẹ để chạy
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar

# Mở cổng 8080
EXPOSE 8080

# Chạy app với profile 'prod' (nếu có) hoặc mặc định
ENTRYPOINT ["java", "-jar", "app.jar"]