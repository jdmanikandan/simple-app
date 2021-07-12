pipeline {
   agent any

   environment {
       // use your actual issuer URL here and NOT the placeholder {yourOktaDomain}
       OKTA_OAUTH2_ISSUER           = 'https://dev-15744589.okta.com/oauth2/ausnt5zqzcrIdMTZN5d6'
       OKTA_OAUTH2_CLIENT_ID        = credentials('OKTA_OAUTH2_CLIENT_ID')
       OKTA_OAUTH2_CLIENT_SECRET    = credentials('OKTA_OAUTH2_CLIENT_SECRET')
   }

   stages {
      stage('Build') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/jdmanikandan/simple-app.git'

            // Run Maven on a Unix agent.
            sh "chmod +x mvnw"
            sh "./mvnw -Dmaven.test.failure.ignore=true clean package"

           sh "./mvnw -Dmaven.test.failure.ignore=true clean package"


            // To run Maven on a Windows agent, use
           // bat "mvn -Dmaven.test.failure.ignore=true clean package"
         }

         post {
            // If Maven was able to run the tests, even if some of the test
            // failed, record the test results and archive the jar file.
            success {
               junit '**/target/surefire-reports/TEST-*.xml'
               archiveArtifacts 'target/*.jar'
            }
         }
      }
   }
}
