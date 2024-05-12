pipeline {
  
  agent any
  
  tools {
    maven 'maven'
  }
  
  stages {
          stage ('Initialize') {
          steps {
          sh '''
                echo "PATH = ${PATH}"
                echo "M2_HOME= ${M2_HOME}"
           '''
                  }
                }
    
          stage ('Build') {
          steps {
        sh 'mvn clean package'
                }
                          }
          stage ('Deploy-To-Tomcat') {
          steps {
          sshagent(['tomcat']) {
            sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@52.66.36.130:/home/ubuntu/prod/apache-tomcat-9.0.89/webapps/webapp.war'
                                } 
                }
                                      }
          }

        }
