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
     //     stage ('Check-Git-Secrets') {
     //     steps {
     //       sh 'rm trufflehog || true'
     //       sh 'docker run gesellix/trufflehog --json https://github.com/raviv935/webapp.git > trufflehog'
     //       sh 'cat trufflehog'
      //          }
       //                               }
      //    stage ('Source Compostition Analysiss') {
      //    steps {
      //      sh 'rm owasp* ||true'
      //      sh 'wget "https://raw.githubusercontent.com/raviv935/webapp/master/owasp-dependency-check.sh" '
      //      sh 'chmod +x owasp-dependency-check.sh'
      //      sh 'bash owasp-dependency-check.sh'
      //      sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
       //         }
                                                  }
          stage ('SAST' ) {
            steps {
              withSonarQubeEnv('SonarQube') {
              sh 'mvn sonar:sonar'
              sh 'cat target/sonar/report-task.txt'
                                            }
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
            sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@65.2.140.102:/prod/apache-tomcat-9.0.89/webapps/webapp.war'
                                } 
                }
                                      }
          }

        }
