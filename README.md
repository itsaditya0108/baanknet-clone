# baanknet clone
# e auction bank


@echo off
setlocal

REM ===== CONFIG =====
set TOMCAT_SERVICE=Tomcat9
set TOMCAT_WEBAPPS=C:\server\apps\tomcat-auth\webapps
set WAR_CONTEXT=authapp
set BUILD_WAR=C:\ProgramData\Jenkins\.jenkins\workspace\auth-service-ci\authapp\target\authapp-0.0.1-SNAPSHOT.war

echo Stopping Tomcat...
net stop %TOMCAT_SERVICE%

echo Cleaning old deployment...
del /f /q "%TOMCAT_WEBAPPS%\%WAR_CONTEXT%.war"
rmdir /s /q "%TOMCAT_WEBAPPS%\%WAR_CONTEXT%"

echo Copying new WAR...
copy /Y "%BUILD_WAR%" "%TOMCAT_WEBAPPS%\%WAR_CONTEXT%.war"

echo Starting Tomcat...
net start %TOMCAT_SERVICE%

endlocal







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

#Actuator

management.endpoints.web.exposure.include=health,info
management.endpoint.health.show-details=always
management.server.base-path=/actuator

