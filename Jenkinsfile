pipeline {
  agent {
    node {
      label 'test'
    }

  }
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.host.url=http://172.31.86.101:9000/ \\
  -Dsonar.projectKey=Petclinic \\
  -Dsonar.login=sqp_cdc961205eb429374d9d007f6a9860fc3f7a8491'''
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
      }
    }

    stage('Package') {
      steps {
        sh './mvnw jar:jar package -DskipTests=true'
      }
    }

    stage('QA') {
      parallel {
        stage('Deploy') {
          steps {
            sh 'java -jar target/*.jar'
          }
        }

        stage('Integration and Performance Tests') {
          steps {
            sh './mvnw verify'
          }
        }

      }
    }

  }
}