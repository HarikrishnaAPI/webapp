pipeline {
  agent any
  tools {
    maven "maven"
  }
  stages {
    stage ("initialize") {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }  
    }
    
    stage ("Buid") {
      sh "mvn clean package" 
    }
  }
}
