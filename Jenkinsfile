pipeline{
    agent any

    stages {

        stage('Git Checkout'){
            steps{
                script{
                    git branch: 'main', url: 'https://github.com/mhulic/jenkins-javaapp.git'
                    gitCheckout{
                        branch: "main",
                        url: "https://github.com/mhulic/jenkins-javaapp.git"
                    }
                }
            }
        }
    }
}