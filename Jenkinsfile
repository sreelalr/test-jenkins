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
                //sh 'terraform init -upgrade'
                
                //sh 'terraform apply --auto-approve'
                
                //sleep(time: 300, unit: "SECONDS")
              
                
                //sh 'terraform destroy --auto-approve'
                
                //sh 'python3 snapshot.py'
                script {
                    def snapshotId = sh(script: 'python3 snapshot.py',returnStdout: true)
                    print(snapshotId)
                }    
                
            }
        }
    }
}   
