pipeline {
    agent any

    stages {
        
        stage('Build') {

            steps {
                withGradle {
                    sh './gradlew assemble'

                }

            }

        }
        
        stage('Test') {
            steps {
                withGradle {
		            sh './gradlew test'
		            configFileProvider([configFile(fileId: 'hello-grails-gradle.properties', targetLocation: 'gradle.properties')]) {
                              sh './gradlew integrationTest'
                    }

                }
		    
		    withSonarQubeEnv(credentialsId: 'c8c23d90-c1f4-4828-910a-97bfca0f6944', installationName: 'local') {
                    sh './gradlew clean sonarqube'
                }

            }

        }


    }
}

