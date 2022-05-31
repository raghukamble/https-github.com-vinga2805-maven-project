pipeline {
    agent any
    parameter {
        string(name:'stage-tomcat',defaultValue:'13.232.232.14',description:'our stage server')
        string(name:'prod-tomcat',defaultValue:'13.232.232.14',description:'our prod server')
    }
    triggers {
        pollSCM(*****)
    }

    stages {
        stage(Build)
            steps {
        echo"Building an Application"
        sh 'mvn compose'
            }

        

    stage {
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

    stage(Deployment) {
        steps {
            echo "Testing Application in Staging Area"
            sh "scp -i /home/jenkins/india.pem **/target/*.war ec2-user@${params.stage-tomcat}:/var/lib/tomcat9/webapps"

        }
    }

    stage(Deployment) {
        steps {
            echo " Deploying Application to the Production"
            sh "scp -i /home/jenkins/india.pem **/target/*.war ec2-user@${params.prod-tomcat}:/var/lib/tomcat9/webapps"
        }
    }

    }
         
}