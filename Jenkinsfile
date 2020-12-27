pipeline {
 agent any
environment {
    registry = "dhana250/eureka-client"
    registryCredential = 'docker'
  }

    stages {
            stage ('Compile Stage') {

                steps {
                echo 'jshdfjkshfjkshf...'
                    withMaven(maven : 'maven_3_6_3') {
                        sh 'mvn clean compile'
                    }
                }
            }

            stage ('Testing Stage') {

                steps {
                echo 'rtyrtytdfyrtrt...'
                    withMaven(maven : 'maven_3_6_3') {
                        sh 'mvn test'
                    }
                }
            }


            stage ('Deployment Stage') {

                steps {
                echo '4564645645645...'
                    withMaven(maven : 'maven_3_6_3') {
                        sh 'mvn deploy'
                    }
                }
            }
      stage('Building image') {
        steps{
          script {
            dockerImage = docker.build registry + ":$BUILD_NUMBER"
          }
        }
      }
      stage('Deploy Image') {
        steps{
          script {
            docker.withRegistry( '', registryCredential ) {
              dockerImage.push()
            }
          }
        }
      }
  }
