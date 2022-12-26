pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', credentialsId: '87c81795-7ea2-4864-9d32-1225f16a5e70', url: 'https://github.com/vasavidilip04/vasavi'
            }
        }
         stage('maven package') {
            steps {
            sh "mvn clean pckage"
            }
        }
        stage('tomcat-deploy') {
            steps {
              sshagent(['tomcat-cred']){
              sh "scp-o stricthostkeychecking=no target/*.war ec2-user@172.31.46.86:/opt/dilip/webapps"
              sh "ssh ec2-user@172.31.46.86 /opt/dilip/bin/showndown.sh."
              sh "ssh ec2-user@172.31.46.86 /opt/dilip/bin/startup.sh."
            
            }
        }
    }
}
