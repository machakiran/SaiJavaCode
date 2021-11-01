pipeline{
  agent any
  stages{
    stage("Git Checkout"){
      steps{
            git credentialsId: 'github', url: 'https://github.com/machakiran/SaiJavaCode.git'
           }
          }
     stage("Maven Build"){
       steps{
            sh "/opt/apache-maven-3.8.3/bin/mvn package"
             }
            }
     stage("deploy-dev"){
       steps{
          sshagent(['18.206.249.222']) {
          sh """
          scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/jenkins3/webapp/target/webapp.war ubuntu@18.206.249.222:/opt/apache-tomcat-8.5.72/webapps 
          ssh ubuntu@18.206.249.222/opt/apache-tomcat-8.5.72/bin/shutdown.sh
          ssh ubuntu@18.206.249.222/opt/apache-tomcat-8.5.72/bin/startup.sh
           """
            }
          }
        }
      }
    }
