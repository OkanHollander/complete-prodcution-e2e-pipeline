pipeline{
    agent{
        docker { image 'node:18.18.0-alpine3.18' }
    }
    tools {
        jdk "Java17"
        maven "Maven3"
    }
    stages{
        stage("Cleanup Workspace"){
            steps{
                cleanWs()
            }
        }
    
        stage("Checkout from SCM"){
            steps{
                git branch: "main", credentialsId: "github", url: "https://github.com/OkanHollander/complete-prodcution-e2e-pipeline.git"
            }
        }

        stage("Build Application"){
            steps{
                sh "mvn clean package"
            }
        }
        
        stage("Test Application"){
            steps{
                sh "mvn test"
            }
        }
    }
}