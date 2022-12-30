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
                        
                          git branch: "main", credentialsId: "git", url: "https://github.com/sreelalr/demo-tf.git"
                        
                    }
                }
            }
        
        stage('Plan') {
            steps {
                sh 'terraform init -upgrade'
                
                sh 'terraform apply --auto-approve'
                
                time.sleep(120)
                
                sh 'terraform destroy --auto-approve'
                
                
            }
        }
    }
}   
