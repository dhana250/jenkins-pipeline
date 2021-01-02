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
     
            def pom = readMavenPom file:'pom.xml'
            echo "${pom.version}"
           dockerImage = docker.build registry + ":$BRANCH_NAME"
         
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
 
 post{
  always{
   echo "Image is pushed always"
  }
  success{
   echo "build is success"
  }
 }
}
