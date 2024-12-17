def FAILED_STAGE

pipeline {
  agent any

  stages {
  
    stage('Build') {
      steps {
        script {
          FAILED_STAGE=env.STAGE_NAME
          sh './mvnw clean package'
        }
      }
    }

    stage('Containerization') {
      steps {
        script {
          FAILED_STAGE=env.STAGE_NAME
          sh """
            docker build -t jobin589/spring-petclinic:${env.BUILD_NUMBER} .
            docker push myimage
          """
        }
      }
    }

  }

  post {
    failure {
      script {
        sh "python read_logs.py"
      }
    }
  }
}
