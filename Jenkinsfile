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
          stage ('Check-Git-Secrets') {
          steps {
            sh 'rm trufflehog || true'
            sh 'docker run gesellix/trufflehog --json https://github.com/raviv935/webapp.git > trufflehog'
            sh 'cat trufflehog'
                }
                                      }
          stage ('Source Compostition Analysis') {
          steps {
            sh 'rm owasp* ||true'
            sh 'wget 'https://raw.githubusercontent.com/r4v1/webapp/master/owasp-dependency-check.sh'
            sh 'chmod +x owasp-dependency-check.sh'
            sh 'bash owasp-dependency-check.sh'
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
            sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@52.66.36.130:/prod/apache-tomcat-9.0.89/webapps/webapp.war'
                                } 
                }
                                      }
          }

        }
