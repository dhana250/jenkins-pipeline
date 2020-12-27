pipeline {
environment {
    registry = "dhana250/eureka-client"
    registryCredential = 'docker'
  }  agent any  stages {

     steps {

                  withMaven(maven : 'maven_3_6_3') {
                      sh 'mvn clean compile'
                  }
              }
          }

          stage ('Testing Stage') {

              steps {

                  withMaven(maven : 'maven_3_6_3') {
                      sh 'mvn test'
                  }
              }
          }
          stage ('package Stage') {

                        steps {

                            withMaven(maven : 'maven_3_6_3') {
                                sh 'mvn package'
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
  }