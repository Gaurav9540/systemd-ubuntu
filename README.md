# systemd-ubuntu

**Run java jar file in background using Systemd**


**Step 1: Copy the JAR to /opt/myapp**

```ssh
mkdir -p /opt/myapp
```

```ssh
cp /root/license_app/target/JWT-with-Spring-Security-0.0.1-SNAPSHOT.jar /opt/myapp/
```

<hr>

**Step 2: Create a systemd Service File**
Create a new service:

```ssh
vim /etc/systemd/system/myapp.service
```

Paste this:

```ssh
Paste this:
[Unit]
Description=License App Service
After=network.target

[Service]
User=root
WorkingDirectory=/opt/myapp
ExecStart=/usr/bin/java -jar /opt/myapp/JWT-with-Spring-Security-0.0.1-SNAPSHOT.jar --server.port=8086
SuccessExitStatus=143
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
```
