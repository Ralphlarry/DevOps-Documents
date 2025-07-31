1. sudo apt update
   
   
# Install Default Jdk
2. sudo apt install default-jdk
   java -version

# Setting up a Tomcat User
3. sudo useradd -r -m -U -d /opt/tomcat -s /bin/false tomcat

# Downloading the Tomcat package
4. wget -c https://downloads.apache.org/tomcat/tomcat-9/v9.0.34/bin/apache-tomcat-9.0.34.tar.gz

# Install Tomcat on Linux
5. sudo tar xf apache-tomcat-9.0.34.tar.gz -C /opt/tomcat
6. sudo ln -s /opt/tomcat/apache-tomcat-9.0.34 /opt/tomcat/updated
7. sudo chown -R tomcat: /opt/tomcat/*

# Permissions Tomcat
8. sudo sh -c 'chmod +x /opt/tomcat/updated/bin/*.sh'

# Configuring the Tomcat service
9. sudo nano /etc/systemd/system/tomcat.service
    
10. # Enter the following in your file and save it. Note that you need to update
    # the value of JAVA_HOME if your Java installation directory is not the same as given below:
    [Unit]
Description=Apache Tomcat Web Application Container
After=network.target

[Service]
Type=forking

Environment="JAVA_HOME=/usr/lib/jvm/java-1.11.0-openjdk-amd64"
Environment="CATALINA_PID=/opt/tomcat/updated/temp/tomcat.pid"
Environment="CATALINA_HOME=/opt/tomcat/updated/"
Environment="CATALINA_BASE=/opt/tomcat/updated/"
Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"
Environment="JAVA_OPTS=-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom"

ExecStart=/opt/tomcat/updated/bin/startup.sh
ExecStop=/opt/tomcat/updated/bin/shutdown.sh

User=tomcat
Group=tomcat
UMask=0007
RestartSec=10
Restart=always

[Install]
WantedBy=multi-user.target


11. sudo systemctl daemon-reload

12. sudo systemctl status tomcat

13. sudo systemctl enable tomcat

# Firewall Rules Tomcat
14. sudo ufw allow 8080/tcp

# Verifying our installation
15. http://<YourIPAddress>:8080
