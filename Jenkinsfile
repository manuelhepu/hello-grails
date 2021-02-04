pipeline {
    agent any

    stages {
        
        stage('Build') {

            steps {
                withGradle {
                    sh 'chmod +x ./gradlew'
                    sh './gradlew assemble'

                }

            }

        }
        
        stage('Test') {
            steps {
                withGradle {
		            sh './gradlew TEST'
		            configFileProvider(
                              [configFile(fileId: 'hello-grails-gradle.properties', targetLocation: 'gradle.properties')]) {
                              sh './gradlew iT'
                    }

                }

            }

            post {
                always {
                    junit 'build/test-results/test/TEST-*.xml'


                    
                }
            }
        }


    }
}

