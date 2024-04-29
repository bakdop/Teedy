pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        // 生成Surefire测试报告
        junit '**/target/surefire-reports/*.xml'
        
        // 生成Javadoc文档
        javadoc javadocOutputDir: 'target/apidocs'
      }
    }
    stage('pmd') {
      steps {
        sh 'mvn pmd:pmd'
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
