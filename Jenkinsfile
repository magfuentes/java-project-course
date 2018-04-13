pipeline {
  agent any

  stages {
    stage('Say Hello') {
      agent any
      
      steps {
       sayHello 'Awesome Student!'  
      }
    } 
    stage(' Unit Tests') {
      steps {
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
     }
    }
    stage('build'){
      steps {
        sh 'ant -f build.xml -v'
      }
    }
  }
  
  post {
    always {
      archiveArtifacts artifacts: 'dist/*.jar ', fingerprint: true
    }
  }
}
