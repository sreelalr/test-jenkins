pipeline {
    agent any

    parameters {
        string(name: 'environment', defaultValue: 'terraform', description: 'Workspace/environment file to use for deployment')
        }

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
                            git branch: 'main', url: "https://github.com/sreelalr/test-jenkins.git"
                        }
                    }
                }
            }
        
        stage('Plan') {
            steps {
                sh 'terraform init -input=false'
                sh 'terraform workspace select ${environment} || terraform workspace new ${environment}'

                sh "terraform plan -input=false -out tfplan "
                sh 'terraform show -no-color tfplan > tfplan.txt'
            }
        }
    }
}   
