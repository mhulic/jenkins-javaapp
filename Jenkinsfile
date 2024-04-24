@Library('jenkins-shared-lib') _

pipeline{

    agent any

    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')
        string(name: 'ImageName', description: "name of the docker build", defaultValue: 'javaapp')
        string(name: 'ImageTag', description: "tag of the docker build", defaultValue: 'v1')
        string(name: 'DockerHubUser', description: "name of the Application", defaultValue: 'testhulic')
        string(name: 'GitRepositary', description: "name of git repo to test the Application", defaultValue: 'https://github.com/mhulic/Calculator.git')
        string(name: 'Branch', description: "name of branch to test the Application", defaultValue: 'main')
    }

    stages{
         
        stage('Git Checkout'){
                    when { expression {  params.action == 'create' } }
            steps{
                gitCheckout(
                    branch: "${params.Branch}",
                    url: "${params.GitRepositary}"
                )
            }
        }

        // stage('Unit test MVN'){
        //             when { expression {  params.action == 'create' } }
        //     steps{
        //         mvnTest(
        //         )
            
        //     }
        // }

        // stage('Integration Test maven'){
        //             when { expression {  params.action == 'create' } }
        //     steps{
        //        script{
        //            mvnIntegrationTest()
        //        }
        //     }
        // }

        // stage('Static code analysis: Sonarqube'){
        //              when { expression {  params.action == 'create' } }
        //     steps{
        //        script{
        //            def SonarQubecredentialsId = 'admin'
        //            statiCodeAnalysis(SonarQubecredentialsId)
        //        }
        //     }
        // }

        // stage('Quality Gate Status Check : Sonarqube'){
        //             when { expression {  params.action == 'create' } }
        //     steps{
        //        script{
                   
        //            def SonarQubecredentialsId = 'admin'
        //            QualityGateStatus(SonarQubecredentialsId)
        //        }
        //     }
        // }

        stage('Maven Build : maven'){
         when { expression {  params.action == 'create' } }
            steps{
               script{
                   mvnBuild()
               }
            }
        }

        stage('Docker Image Build'){
            when { expression {  params.action == 'create' } }
            steps{
               script{
                   
                   dockerBuild("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
               }
            }
        }

        stage('Docker Image Scan: trivy '){
         when { expression {  params.action == 'create' } }
            steps{
               script{
                   
                   dockerImageScan("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
               }
            }
        }

    }
}