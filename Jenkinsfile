pipeline {
    agent any

    triggers {
        //pollSCM trigger to poll every 2 minutes.
        pollSCM('*/2 * * * *')


    }

    stages {
        stage('Build') {
            steps {
                echo "Building an Application"
                sh 'mvn compile'
            }
        }

    stage('Packaging') {
            steps {
                echo "Packaging an Application"
                sh 'mvn clean package'
            }
        post {
            success {
                echo "Archiving the Artifacts"
                archiveArtifacts artifacts:'**/*.war'
            }
         }
         
        }
    stage('Deployment') {
            steps {
                echo "Deploying an Application"
                sh "scp -i /var/lib/jenkins/pick.pem **/target/*.war ec2-65-0-129-138.ap-south-1.compute.amazonaws.com:/usr/local/tomcat9/webapps/"
            }
        }


    }


}
