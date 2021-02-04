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
                    sh './gradlew test'
		    sh './gradlew -Dgeb.env=firefoxHeadless iT'

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

