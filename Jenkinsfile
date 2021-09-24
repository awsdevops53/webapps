pipeline{
  agent any
}
stages{
  stage("Git checkout"}{
    steps{
      git credentialsId: '8cdac168-8725-452a-8c46-10fddf82eb8d', url: 'https://github.com/awsdevops53/webapps.git
    }
  }
  stage("Maven Build"){
    steps{
      sh "mvn clean package"
      sh "mv /var/lib/jenkins/workspace/sample/target/*.war myweb.war
      
    }  
  }   
  stage("deploy-test"){
    steps{
      sshagent(['tomcat-test]) {
      sh """
      scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/sample/target/*.war myweb.war ec2-user@172.31.19.212:/home/ec2-user/apache-tomcat-9.0.53/webapps
      ssh ec2-user@172.31.19.212 /home/ec2-user/apache-tomcat-9.0.53/bin/shutdown.sh
      ssh ec2-user@172.31.19.212 /home/ec2-user/apache-tomcat-9.0.53/bin/startup.sh
      
      """
    }
    }
  }
 }
}
