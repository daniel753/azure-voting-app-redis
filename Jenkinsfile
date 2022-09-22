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
               script{docker.withRegistry("https://hub.docker.com", "DockerHub"){
                  def image = docker.build("pixerflame/jenkins-course:latest")
            image.push()
               }
      }

     
      // stage('Start test app') {
      //    steps {
      //       sh(script: """
      //          docker-compose up -d
      //          ./scripts/test_container.sh
      //       """)
      //    }
      //    post {
      //       success {
      //          echo "App started successfully :)"
      //       }
      //       failure {
      //          echo "App failed to start :("
      //       }
      //    }
      // }
      // stage('Run Tests') {
      //    steps {
      //       sh(script: """
      //          pytest ./tests/test_sample.py
      //       """)
      //    }
      // }
      // stage('Stop test app') {
      //    steps {
      //       sh(script: """
      //          docker-compose down
      //       """)
      //    }
      // }   
   }
}
