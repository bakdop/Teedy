pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Docs'){
      steps{
        sh 'mvn javadoc:jar'
      }
    }
    stage('Test report'){
      steps{
        sh 'mvn surefire-report:report'
      }  
    }
  }  
  post {
    always {
      archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
      archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
      archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
    }
  }
}



