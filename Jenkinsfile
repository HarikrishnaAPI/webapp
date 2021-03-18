pipeline {
  agent any 
  tools {
    maven 'apache-maven-3.6.3'
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

    stage ('Build') {
      steps {
      bat 'mvn clean package'
       }
    }
  }
}
