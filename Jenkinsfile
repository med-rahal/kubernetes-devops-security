pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //so that they can be downloaded later
            }
        }  
      stage('unit tests') {
            steps {
              sh "mvn test"
            }
            post {
              always {
                junit 'target/surefire-reports/*.xml'
                jacoco execPattern: 'target/jacoco.exec'
              }
            }
        } 
      stage('Build Artifact - Maven') {
            steps {
            sh "mvn clean package -DskipTests=true"
            archive 'target/*.jar'
      }
      }  
      stage('Docker Build and Push') {
            steps {
            sh "printenv"
            sh "docker build -t siddhart67/numeric-app:""$GIT_COMMIT" //comment
            sh "printenv"
      }
      } 

    }
}