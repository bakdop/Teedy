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
      // 生成Surefire测试报告
      steps{
        sh'mvn surefire-report:report'
      }  
    }
    stage('Docs'){
       // 生成Javadoc文档
      steps{
        sh'javadoc -d .\javadoc -author -version -encoding UTF-8 -charset UTF-8 example_01.java'
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
