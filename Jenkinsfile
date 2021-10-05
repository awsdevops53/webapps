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
     sh scp -p /home/ec2-user/apache-maven-3.8.2/web-project/target/web-project.war ec2-user@18.234.161.177:/home/ec2-user/apache-tomcat-10.0.11/webapps
     sh ssh ec2-user@18.234.161.177 /home/ec2-user/apache-tomcat-10.0.11/bin/shutdown.sh
     sh ssh ec2-user@18.234.161.177 /home/ec2-user/apache-tomcat-10.0.11/bin/startup.sh
      
      """
     }
     }
  }
}
}
