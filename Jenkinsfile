pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('pmd') {
      steps {
        sh 'mvn pmd:pmd'
      }
    }
    stage('Test report'){
     
      steps{
        sh 'mvn surefire-report:report'
      }  
    }
    stage('Docs'){
      
      steps{
        sh 'javadoc -d .\javadoc -author -version -encoding UTF-8 -charset UTF-8 example_01.java'
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



