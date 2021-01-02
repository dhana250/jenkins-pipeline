pipeline {
 agent any
 environment {
     registry = "dhana250/eureka-client"
     registryCredential = 'jenkins-docker'
     dockerImage =''
  def pom = readMavenPom()

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
         def pom = readMavenPom 'pom.xml'
         echo "{pom}"
          script {
            echo version
           dockerImage = docker.build registry + ":${pom}"
         
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
