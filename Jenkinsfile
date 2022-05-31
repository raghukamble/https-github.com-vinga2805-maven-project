pipeline {
    agent any

    triggers {
        pollSCM('*****')


    }

    stages {
        stage('Build') {
            steps {
                echo "Building an Application"
                sh 'mvn compose'
            }
        }

    stage('Packaging') {
            steps {
                echo "Packaging an Application"
                sh 'mvn clean package'
            }
        }

        post {
            success {
                echo "Archiving the Artifacts"
                archiveArtifacts artifacts:'**/*.war'
            }
        }
    }


    }
