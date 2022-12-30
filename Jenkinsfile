pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

    stages {
        stage('checkout') {
            steps {
                 script{
                        dir("terraform")
                        {
                            git branch: "main", credentialsId: "git", url: "https://github.com/sreelalr/demo-tf.git"
                        }
                    }
                }
            }
        
        stage('Plan') {
            steps {
                sh 'terraform init'

                sh "terraform plan -out tfplan "
                sh 'terraform show -no-color tfplan > tfplan.txt'
                sh 'cat tfplan.txt'
            }
        }
    }
}   
