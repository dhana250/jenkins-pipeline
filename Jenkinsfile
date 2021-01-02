pipeline {
 agent any
 environment {
     registry = "dhana250/eureka-client"
     registryCredential = 'jenkins-docker'
     dockerImage =''
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


            stage ('Package Stage') {

                steps {
                echo '4564645645645...'
                    withMaven(maven : 'maven_3_6_3') {
                        sh 'mvn package'
                    }
                }
            }
      stage('Building image') {
        steps{
          script {
            dockerImage = docker.build registry + ":$BUILD_NUMBER"
           echo '${dockerImage}'
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
