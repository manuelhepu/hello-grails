pipeline {
    agent any

    stages {
        
        stage('Build') {
            configFileProvider ([configFile ( fileId : hello-grails-gradle.properties, variable : ' PACKER_OPTIONS ' )]) {
                        echo " =========== ^^^^^^^^^^^^ Leyendo la configuración del script de canalización "
                        sh " cat $ { env.PACKER_OPTIONS } "
                        echo " ======= ==== ~~~~~~~~~~~~ ============ "

                    }
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

