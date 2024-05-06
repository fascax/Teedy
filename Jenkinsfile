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
      archiveArtifacts artifacts: '**/target/site/**', fingerprint: true // PMD, Surefire reports, etc.
      archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true // Includes the generated Javadoc JAR
      archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
    }
  }
}
