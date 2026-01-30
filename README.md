# baanknet clone
# e auction bank


@echo off
echo Stopping Tomcat...
net stop "Apache Tomcat 9.0"

echo Cleaning old deployment...
del /f /q "C:\server\apps\tomcat-auth\webapps\auth-service.war"
rmdir /s /q "C:\server\apps\tomcat-auth\webapps\auth-service"

echo Copying new WAR...
copy /Y "auth-service\target\auth-service.war" "C:\server\apps\tomcat-auth\webapps\auth-service.war"

echo Starting Tomcat...
net start "Apache Tomcat 9.0"



spring.application.name=authapp
server.port=8080

# DB
spring.datasource.url=jdbc:mysql://localhost:3306/auth_service
spring.datasource.username=auth_user
spring.datasource.password=YOUR_DB_PASSWORD
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

spring.jpa.hibernate.ddl-auto=validate
spring.jpa.show-sql=false
spring.jpa.open-in-view=false

# Logs
logging.file.name=C:/server/data/logs/auth-service/authapp.log
logging.level.root=INFO

# JWT (example)
security.jwt.secret=CHANGE_THIS_SECRET
security.jwt.expiry=3600
