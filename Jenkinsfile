pipeline {
    Agent any
    
        Stages { 

            stage('Build') {
                steps {
                 sh 'mvn -B -DskipTests clean package'
                        }
                          }

            stage('Test') {
                    steps {
                sh 'mvn test'
                    }
         
                    }

            stage('SonarQube Analytics') {
                steps {
                    // mvnHome =  tool name: 'apache-maven-3.6.1', type: 'maven'
                 withSonarQubeEnv('sonar7') { 
   //              sh "${mvnHome}/bin/mvn sonar:sonar"
                sh "mvn sonar:sonar"
        //        withSonarQubeEnv('sonar-server') {
          //          sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
                            }
                          }
                      }
                     

            stage('Slack Notification'){
             steps{
                script{
                //slackSend channel: '#jenkins-build', color: 'Good', message: 'Welcome to Jenkins', teamDomain: 'x0c0x', tokenCredentialId: 'slacknotification'
               // slackSend color: 'good', message: 'Build is successfully completed', channel: '#jenkins-build'
              //  slackSend (color: 'good', channel: '#jenkins-build', message: "Completed: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
    
	currentBuild.result = 'SUCCESS'
        message = """
        *Jenkins Build*
        Job name: `${env.JOB_NAME}`
        Build number: `#${env.BUILD_NUMBER}`
        Build status: `${currentBuild.result}`
        Build details: <${env.BUILD_URL}/console|See in web console>
    """.stripIndent()
	slackSend(color: 'good', message: message)
			            }
			        }
		     }

                           
        }    

}
