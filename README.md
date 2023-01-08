####
### Prerequisites
- JDK 1.8 or later
- Maven 3 or later
- 
### Working OF Project
Technologies used -> Git, AWS, Jenkins, Nexus, SonarQube, Slack

AWS:
 - Create 3 EC2 instances for Jenkins, Nexus, SonarQube and pass script which is in userdata directory
 - validate all the service is up and running using Systemctl status command

Git:
- upload App code on git hub
- create webhook for jenkins so build can be automatically triggered.

Jenkins:
- download required plugins 
  1. Pipeline Utility Steps
  2. Build TimeStamp
  3. Slack Notification
  4. Nexus Artifact Uploader
  5. Sonarqube Scanner
  6. Github plugin

- Manage all credentials using manage credentials

Nexus:
- create Maven- hosted repo

SonarQube:
- create sonarqube webook and integrate with jenkins and create Quality gates



