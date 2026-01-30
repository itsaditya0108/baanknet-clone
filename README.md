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
