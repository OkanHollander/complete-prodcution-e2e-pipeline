pipeline{
    agent{
        label "Jenkins-agent"
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
                git branch: "main", credentialsId: "GitHub-credentials", url: "https://github.com/OkanHollander/complete-prodcution-e2e-pipeline.git"
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

        stage("Sonarqube Analysis"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') {
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }
    }
}