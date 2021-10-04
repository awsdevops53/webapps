pipeline{
  agent any

stages{
  stage("Git checkout"){
    steps{
      git credentialsId: 'devops', url: 'https://github.com/awsdevops53/webapps.git'
    }
  }
  stage("Maven Build"){
    steps{
      sh "mvn clean package"
      
    }  
  }   
  stage("deploy-test"){
    steps{
      sshagent(['tomcat-test']) {
      sh """
      scp -o StrictHostKeyChecking=no /home/ec2-user/apache-maven-3.8.2/web-project/target/*.war myweb.war ec2-user@54.152.215.91:/home/ec2-user/apache-tomcat-10.0.11/webapps
      ssh ec2-user@54.152.215.91 /home/ec2-user/apache-tomcat-10.0.11/bin/shutdown.sh
      ssh ec2-user@54.152.215.91 /home/ec2-user/apache-tomcat-10.0.11/bin/startup.sh
      
      """
     }
     }
  }
}
}  
