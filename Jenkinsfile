pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

    stages {
        stage('Checkout') {
            steps {
                 script{
                        
                          git branch: "main", credentialsId: "git", url: "https://github.com/sreelalr/demo-tf.git"
                        
                    }
                }
            }
        
        stage('Create snapshot') {
            steps {
                script {
                    def snapshotId = sh(script: 'python3 snapshot.py',returnStdout: true)
                    print(snapshotId)
                }  
                
            }
        }
        stage('Upgrade QA DB from the latest snapshot') {
            steps {
                script {
                    //sleep(time: 300, unit: "SECONDS")
                
                    //sh 'terraform init -upgrade'
                
                    //sh 'terraform taint aws_db_instance.qa_replica3'
                
                    //sh 'terraform taint aws_db_instance.qa_replica2'
                
                    //sh 'terraform apply --auto-approve'
                }
            }
        }
    }
}   
