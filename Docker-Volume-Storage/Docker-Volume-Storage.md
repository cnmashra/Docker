# Docker-Volume-Storage


### Command to list or to view the Docker volume
```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker volume ls
DRIVER    VOLUME NAME
local     0b7d4f354991abfe12d285026a5d1f11ca356aac752457a68a43d98805109060
local     01b5cb022100901dd95b64bec3d64fb3e82f8525d7a83208dcc087ef43325b9a
local     29d2a6acba76e16700968396ee9270b8dc2c9eafcab67bdf87849d6ed1aa3177
local     94a58d60cb6b28ac803a59432acdf870d35abee35f0d059adabd82d3f88de8b2
local     0936d1db4329c5eb38b48782c589e1cd1ff13fd82c496d2972e15f38d46e073c
local     5876b86db849862ca7fdea78414336adc64243973503dfd47ab1f9a0b49ca86c
local     125010fd2e778370ab37da9884ef55817663b88038de498d8e81b7d062a8c516
local     1835845a80bc9b9ce1fc0b19055a22e2336fcf38dce065637310fa257df267bf
local     ffccba4526943f880e94d555b187059dfce91b9984dfcabda45a877e8b3c5176

```

### Command to create the Docker volume manually

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker volume create mysql-data
mysql-data

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker volume ls
DRIVER    VOLUME NAME
local     0b7d4f354991abfe12d285026a5d1f11ca356aac752457a68a43d98805109060
local     01b5cb022100901dd95b64bec3d64fb3e82f8525d7a83208dcc087ef43325b9a
local     29d2a6acba76e16700968396ee9270b8dc2c9eafcab67bdf87849d6ed1aa3177
local     94a58d60cb6b28ac803a59432acdf870d35abee35f0d059adabd82d3f88de8b2
local     0936d1db4329c5eb38b48782c589e1cd1ff13fd82c496d2972e15f38d46e073c
local     5876b86db849862ca7fdea78414336adc64243973503dfd47ab1f9a0b49ca86c
local     125010fd2e778370ab37da9884ef55817663b88038de498d8e81b7d062a8c516
local     1835845a80bc9b9ce1fc0b19055a22e2336fcf38dce065637310fa257df267bf
local     ffccba4526943f880e94d555b187059dfce91b9984dfcabda45a877e8b3c5176
local     mysql-data
```
#### Command to check the mount point created path
```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker inspect mysql-data
[
    {
        "CreatedAt": "2025-10-09T23:46:22Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/mysql-data/_data",
        "Name": "mysql-data",
        "Options": null,
        "Scope": "local"
    }
]
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker %
```
### command to attch the volume mount while creting the docker (-v means volume)

```
REMOVED TE OLD MYSQL CONTAINER

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker ps
CONTAINER ID   IMAGE                     COMMAND                  CREATED       STATUS       PORTS                                         NAMES
701f2e909c5d   two-tier-backend:latest   "python app.py"          8 hours ago   Up 8 hours   0.0.0.0:5001->5000/tcp, [::]:5001->5000/tcp   sad_heisenberg
99993893f495   mysql                     "docker-entrypoint.s…"   8 hours ago   Up 8 hours   3306/tcp, 33060/tcp                           mysql
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker stop 99993893f495 && docker rm 99993893f495
99993893f495
99993893f495

CREATE MYSQL CONTAINER WITH ATTCHING VOLUME [ -v mysql-data:/var/lib/mysql ]

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker run -d --name mysql --network two-tier -v mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops mysql
2c8b3a2b123790d832d934a0f670eea41939d538e143110e2492abbbd9d425d4


RESTARTED THE TWO-TIER CONTAINER

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker restart 701f2e909c5d
701f2e909c5d

```

### command to check the Mountpoint volume in the laptop

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker inspect mysql-data
[
    {
        "CreatedAt": "2025-10-09T23:46:22Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/mysql-data/_data",
        "Name": "mysql-data",
        "Options": null,
        "Scope": "local"
    }
]
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % cd /var/lib/docker/volumes/mysql-data/_data
cd: no such file or directory: /var/lib/docker/volumes/mysql-data/_data
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % sudo su
Password:
sh-3.2# cd /var/lib/docker/volumes/mysql-data/_data
sh: cd: /var/lib/docker/volumes/mysql-data/_data: No such file or directory
sh-3.2#

sh-3.2# exit
exit
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker ps       
CONTAINER ID   IMAGE                     COMMAND                  CREATED         STATUS         PORTS                                         NAMES
5f2c2668624c   mysql                     "docker-entrypoint.s…"   8 minutes ago   Up 8 minutes   3306/tcp, 33060/tcp                           mysql
701f2e909c5d   two-tier-backend:latest   "python app.py"          8 hours ago     Up 8 minutes   0.0.0.0:5001->5000/tcp, [::]:5001->5000/tcp   sad_heisenberg
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker exec -it 5f2c2668624c bash
bash-5.1# ls /var/lib/docker/volumes/mysql-data/_data
ls: cannot access '/var/lib/docker/volumes/mysql-data/_data': No such file or directory
bash-5.1# sudo su
bash: sudo: command not found
bash-5.1# mysql -u root -proot
mysql: [Warning] Using a password on the command line interface can be insecure.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 14
Server version: 9.4.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use devops;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> select * from messages;
+----+------------------------------------------------------------------+
| id | message                                                          |
+----+------------------------------------------------------------------+
|  1 | created the mysql with volume mount point storage                |
|  2 | even mysql container removed data will be there in docker volume |
+----+------------------------------------------------------------------+
2 rows in set (0.001 sec)

mysql> exit
Bye
bash-5.1# exit
exit

What's next:
    Try Docker Debug for seamless, persistent debugging tools in any container or image → docker debug 5f2c2668624c
    Learn more at https://docs.docker.com/go/debug-cli/
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker %

```

## Steps to check the volume mount point in MAC laptop

### 🧠 Option 1: Use the Docker Desktop GUI

1. Open Docker Desktop.

2. Go to the "Volumes" tab on the left sidebar.

3. Search for mysql-data.

4. Click it — you can browse or delete the data right from the GUI.

### 🧠 Option 2: Get the Path Inside the Docker VM

If you want to explore the actual VM:

```
docker run --rm -it --privileged --pid=host justincormack/nsenter1

```

Then inside, you can:
```
cd /var/lib/docker/volumes/mysql-data/_data
ls
```

logs

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % docker run --rm -it --privileged --pid=host justincormack/nsenter1

Unable to find image 'justincormack/nsenter1:latest' locally
latest: Pulling from justincormack/nsenter1
726619a9fa8c: Pull complete 
Digest: sha256:e876f694a4cb6ff9e6861197ea3680fe2e3c5ab773a1e37ca1f13171f7f5798e
Status: Downloaded newer image for justincormack/nsenter1:latest
sh-5.2# cd /var/lib/docker/volumes/mysql-data/_data
sh-5.2# ls
'#ib_16384_0.dblwr'   auto.cnf	      binlog.index      client-key.pem	 ibtmp1       mysql_upgrade_history   server-cert.pem   undo_002
'#ib_16384_1.dblwr'   binlog.000001   ca-key.pem        devops		 mysql	      performance_schema      server-key.pem
'#innodb_redo'	      binlog.000002   ca.pem	        ib_buffer_pool	 mysql.ibd    private_key.pem	      sys
'#innodb_temp'	      binlog.000003   client-cert.pem   ibdata1		 mysql.sock   public_key.pem	      undo_001
sh-5.2#
```

### 🧠 Option 4: Export Volume Data (optional)

If you want to copy data out to your Mac filesystem:

```
docker run --rm \
  -v mysql-data:/volume \
  -v $(pwd):/backup \
  alpine tar czf /backup/mysql_data_backup.tar.gz -C /volume .
```


### ✅ Summary

```
| Task                 | Command or Action                                                                                                      |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Explore contents     | `docker run -it --rm -v mysql-data:/data alpine /bin/sh`                                                               |
| GUI access           | Docker Desktop → Volumes tab                                                                                           |
| See inside Docker VM | `docker run --rm -it --privileged --pid=host justincormack/nsenter1`                                                   |
| Backup volume data   | `docker run --rm -v mysql-data:/volume -v $(pwd):/backup alpine tar czf /backup/mysql_data_backup.tar.gz -C /volume .` |


```

# Groovy script for backup

### Perfect 👌 — here’s a simple and production-friendly Groovy Jenkins pipeline script that:

1. Checks if a Docker volume (e.g. mysql-data) exists.

2. Prints the mount info.

3. If the volume does not exist, it fails the pipeline and notifies via console (and optionally Teams/Slack later).

### ✅ Groovy Jenkinsfile — Check Docker Volume Health

```
pipeline {
    agent any

    environment {
        DOCKER_VOLUME = "mysql-data"
    }

    stages {
        stage('Check Docker Volume Health') {
            steps {
                script {
                    echo "🔍 Checking if Docker volume '${DOCKER_VOLUME}' exists..."

                    // Check if the volume exists
                    def volumeCheck = sh(script: "docker volume inspect ${DOCKER_VOLUME} >/dev/null 2>&1", returnStatus: true)

                    if (volumeCheck == 0) {
                        echo "✅ Docker volume '${DOCKER_VOLUME}' found!"

                        // Show details
                        sh """
                        echo '📦 Volume Details:'
                        docker volume inspect ${DOCKER_VOLUME}
                        """
                    } else {
                        echo "❌ Docker volume '${DOCKER_VOLUME}' not found! Failing pipeline..."
                        error("Docker volume '${DOCKER_VOLUME}' does not exist.")
                    }
                }
            }
        }
    }

    post {
        failure {
            echo "🚨 Pipeline failed! Sending notifications..."

            // 🔹 Example for Teams notification (optional)
            // Replace <WEBHOOK_URL> with your MS Teams Incoming Webhook URL
            sh '''
            curl -H 'Content-Type: application/json' \
                 -d '{"text": "🚨 Jenkins Alert: Docker volume check failed for volume '${DOCKER_VOLUME}'"}' \
                 https://outlook.office.com/webhook/<WEBHOOK_URL>
            '''

            // 🔹 Example for Slack notification (optional)
            // Replace <SLACK_WEBHOOK_URL> with your Slack Incoming Webhook URL
            sh '''
            curl -X POST -H 'Content-type: application/json' \
                 --data '{"text":"🚨 Jenkins: Docker volume '${DOCKER_VOLUME}' not found!"}' \
                 <SLACK_WEBHOOK_URL>
            '''
        }
        success {
            echo "🎉 Docker volume health verified successfully!"
        }
    }
}

```

### 🧠 How It Works

```
| Step                       | Description                                  |
| -------------------------- | -------------------------------------------- |
| `docker volume inspect`    | Checks if the specified Docker volume exists |
| `returnStatus: true`       | Returns 0 if found, 1 if not found           |
| `error()`                  | Fails the Jenkins stage gracefully           |
| `post { failure { ... } }` | Triggers notifications if pipeline fails     |

```

### 🧩 Optional Add-ons

You can extend this:

1. To check multiple volumes by looping through a list.

2. To send rich Teams cards or Slack blocks (for better formatted alerts).

3. To also verify the mount point and data path integrity.


Excellent 👍 — here’s the enhanced Jenkins Groovy pipeline that checks multiple Docker volumes, summarizes the results, and sends notifications if any volume is missing or unhealthy.

This version is perfect for SRE / DevOps health monitoring pipelines — runs in Jenkins, verifies infrastructure state, and can alert via Teams and Slack when issues are detected.

## 🧩 Jenkinsfile — Multi-Volume Docker Health Check with Notifications

```
pipeline {
    agent any

    environment {
        // List of Docker volumes to verify
        DOCKER_VOLUMES = "mysql-data redis-data app-logs"
        TEAMS_WEBHOOK = "https://outlook.office.com/webhook/<YOUR_TEAMS_WEBHOOK_URL>"
        SLACK_WEBHOOK = "https://hooks.slack.com/services/<YOUR_SLACK_WEBHOOK_URL>"
    }

    stages {
        stage('Check Docker Volumes Health') {
            steps {
                script {
                    def missingVolumes = []
                    def healthyVolumes = []

                    echo "🔍 Checking Docker volume health status...\n"

                    for (vol in DOCKER_VOLUMES.tokenize()) {
                        def status = sh(script: "docker volume inspect ${vol} >/dev/null 2>&1", returnStatus: true)

                        if (status == 0) {
                            echo "✅ Volume '${vol}' exists and is healthy."
                            healthyVolumes << vol
                        } else {
                            echo "❌ Volume '${vol}' is missing or corrupted."
                            missingVolumes << vol
                        }
                    }

                    // Print summary
                    echo "\n📦 Docker Volume Health Summary:"
                    echo "--------------------------------"
                    echo "Healthy Volumes: ${healthyVolumes}"
                    echo "Missing Volumes: ${missingVolumes}"

                    // Fail the build if any volume is missing
                    if (missingVolumes.size() > 0) {
                        currentBuild.result = 'FAILURE'

                        // Send notifications
                        def message = """
🚨 *Jenkins Alert - Docker Volume Health Check Failed!*
*Missing Volumes:* ${missingVolumes}
*Healthy Volumes:* ${healthyVolumes}
"""

                        // Microsoft Teams Notification
                        sh """
                        curl -H 'Content-Type: application/json' \
                             -d '{"text": "${message.replaceAll('"','\\"')}"}' \
                             ${TEAMS_WEBHOOK}
                        """

                        // Slack Notification
                        sh """
                        curl -X POST -H 'Content-type: application/json' \
                             --data '{"text": "${message.replaceAll('"','\\"')}"}' \
                             ${SLACK_WEBHOOK}
                        """

                        error("❌ One or more Docker volumes are missing. See summary above.")
                    } else {
                        echo "🎉 All Docker volumes are healthy!"
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ All volumes are present and healthy."
        }
        failure {
            echo "🚨 Jenkins pipeline failed — missing Docker volumes detected."
        }
    }
}

```

### 🧠 What This Script Does

```
| Step                              | Description                                    |
| --------------------------------- | ---------------------------------------------- |
| `DOCKER_VOLUMES`                  | List of volumes to check — space-separated     |
| `docker volume inspect`           | Verifies existence of each volume              |
| `missingVolumes`                  | Stores volumes that failed the check           |
| `Teams & Slack notifications`     | Sends formatted alert messages                 |
| `currentBuild.result = 'FAILURE'` | Marks pipeline failed if any volume is missing |

```

### 📬 Example Notification Message

Teams / Slack Alert:

```
🚨 Jenkins Alert - Docker Volume Health Check Failed!
Missing Volumes: [redis-data]
Healthy Volumes: [mysql-data, app-logs]

```


### ✅ How to Use

1. Replace the <YOUR_TEAMS_WEBHOOK_URL> and <YOUR_SLACK_WEBHOOK_URL> values.

2. Save as Jenkinsfile in your repo or Jenkins job.

3. Run the pipeline — it will automatically detect missing volumes.
