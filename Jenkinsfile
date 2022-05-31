pipeline {
    agent any
    parameter {
        string(name: 'stage-tomcat',defaultValue:'13.232.232.14',description:'our stage server')
        string(name: 'prod-tomcat',defaultValue:'13.232.232.14',description:'our prod server')
    }
    triggers {
        pollSCM('*****')
    }

    stages {
        stage('Build') {
            steps {
        echo"Building an Application"
        sh 'mvn compose'
            }

    }    

    stage('Packaging') {
        steps {
            echo "Packaging Application"
            sh 'mvn clean package'
        }
    }

    post {
        success {
            echo "Publishing the artifacts"
            archiveArtifacts artifacts: '**/*.war'
        }
    }
 }
