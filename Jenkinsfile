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
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    stage('check-git-secret') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/HarikrishnaAPI/webapp.git > trufflehog'
        sh 'cat trufflehog'
      }
    }
    stage('source-compensation-analyser') {
      steps{
        sh 'rm owasp || true'
        sh 'wget "https://raw.githubusercontent.com/HarikrishnaAPI/webapp/master/owasp-dependency-check.sh" '
        sh 'chmod -x owasp-dependency-check.sh'
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
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.234.34.64:/home/ubuntu/apache-tomcat-8.5.64/webapps/webapp.war'
              }      
           }       
    }
  }
}
