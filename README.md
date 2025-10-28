# systemd-ubuntu

**Run java jar file in background using Systemd**

<hr>

🧩 **What is systemd ?**

systemd is the system and service manager used by modern Linux distributions — including Ubuntu (from version 15.04 onward).

It is the first process (PID 1) that runs when the system boots and is responsible for:

 - Starting and stopping all other system services
 - Managing dependencies between services
 - Handling system startup and shutdown
 - Logging (via journald)
 - Mounting filesystems
 - Managing targets (runlevels)
 - Think of systemd as the “brain” of your Linux system startup and service management.

⚙️ **Key Features of systemd**

 -  **Service Management** - Controls all background services (systemctl start/stop/status)  <br>
 - **Parallel Boot** - Starts multiple services at once for faster boot times  <br>
 - **Dependency Handling** - Ensures services start in the correct order  <br>
 - **Logging (journald)** - Centralized system logging  <br>
 - **Targets (like runlevels)** - Define system states (e.g., multi-user.target, graphical.target)  <br>
 - **Timers** - Replace cron jobs for scheduled tasks (.timer units)  <br>

<hr>

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

<hr>

**Step 3: Enable and Start the Service**

```ssh
systemctl daemon-reload
```

```ssh
systemctl enable myapp.service
```

```ssh
systemctl start myapp.service
```

<hr>

**Step 4: Check Status and Logs**

```ssh
systemctl status myapp.service
```

<hr>

**Step 8: Confirm It’s Running on Port 8086**

```ssh
lsof -i :8086
```

<hr>

**Step 9: Check all running services on ubuntu**

```ssh
systemctl list-units --type=service --state=running
```


