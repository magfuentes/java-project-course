pipeline {
  agent any

  stages {
    stage('Say Hello') {
      agent any
      
      steps {
       sayHello 'Awesome Student!'  
      }
    } 
    stage('SAUDACAO'){
     steps {
       sh 'echo "Notification Time!" '
     }
    }
    stage ('Git Information') {
      agent any

      steps {
        echo "My Branch Name : ${env.BRANCH_NAME}"

        script {
          def myLib = new linuxacademy.git.gitStuff();
           
          echo "My Commit: ${myLib.gitCommit("${env.WORKSPACE}/.git")}" 
        } 
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
    success {
      emailext (
         subject: "${env.JOB_NAME} [${env.BUILD_NUMBER}] RAN!",
         body: """ '${env.JOB_NAME} [${env.BUILD_NUMBER}]' Ran!" :Check console output at ${env.JOB_NAME} [${env.BUILD_NUMBER}]/a>""", to: "magfuentes@gmail.com")
    }
    always {
      archiveArtifacts artifacts: 'dist/*.jar ', fingerprint: true
    }
  }
}
