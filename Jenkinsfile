@Library('jenkins-shared-lib') _

pipeline{

    agent any

    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')
        string(name: 'ImageName', description: "name of the docker build", defaultValue: 'javaapp')
        string(name: 'ImageTag', description: "tag of the docker build", defaultValue: 'v1')
        string(name: 'DockerHubUser', description: "name of the Application", defaultValue: 'testhulic')
        string(name: 'Branch', description: "nameBranch to test the Application", defaultValue: 'main')
    }

    stages{
         
        stage('Git Checkout'){
                    when { expression {  params.action == 'create' } }
            steps{
                gitCheckout(
                    branch: "main",
                    url: "https://github.com/mhulic/Calculator.git"
                )
            }
        }

        stage('Unit test MVN'){
                    when { expression {  params.action == 'create' } }
            steps{
                mvnTest(
                )
            
            }
        }

    }
}