pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('PMD') {
      steps {
        sh 'mvn pmd:pmd'
      }
    }
    stage('Generate Javadoc') {
      steps {
        sh 'mvn javadoc:jar' 
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test' 
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: '**/target/pmd.xml', fingerprint: true
      archiveArtifacts artifacts: '**/target/surefire-reports/**', fingerprint: true

      archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
      archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
      archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
    }
  }
}
