pipeline {
  agent any
  stages {
    stage('Clean Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.projectKey=petclinic-latest \\
  -Dsonar.projectName=\'petclinic-latest\' \\
  -Dsonar.host.url=http://3.26.20.79:9001 \\
  -Dsonar.token=sqp_cd255f4e0abe3f3d92ee581d4a4f6b312fbb99fe'''
      }
    }

    stage('Unit Tests') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
      }
    }

  }
}