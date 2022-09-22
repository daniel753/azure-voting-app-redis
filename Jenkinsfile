pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }

       stage('Docker build') {
         steps {
            sh(script: """
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd
            """)
         }
      } 

      stage("Push Container to dockerhub"){
         steps{
            echo "Workspace is $WORKSPACE"
            dir("$WORKSPACE/azure-vote"){
               script{docker.withRegistry('https://index.docker.io/v1/', 'DockerHub'){
                  def image = docker.build("pixerflame/jenkins-course:v1")
                  image.push()
               }
            }
        }
      }
   }
}
}