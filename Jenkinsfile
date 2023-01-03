pipeline {
    agent any
    
    
    parameters{
            string(defaultValue: 'us-west-2', description: 'aws region', name: 'awsRegion')
            string(defaultValue: 'hp-altuscare',description: 'db identifier', name: 'dbId')
    }
    

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
                    def snapshotId = 'for-qa-' + new Date().format('yyyy-MM-dd')
                    print(snapShotId)
                    
                    aws rds create-db-snapshot --db-snapshot-identifier "$snapshotId" --db-instance-identifier "$params.dbId" --region "$params.awsRegion"
                    //def snapshotId = sh(script: "python3 snapshot.py '$params.awsRegion' '$params.dbId'",returnStdout: true)
                    //print(snapshotId)
                }  
                
            }
        }
        stage('Upgrade QA DB from the latest snapshot') {
            steps {
                script {
                    sleep(time: 30, unit: "SECONDS")
                
                    //sh 'terraform init -upgrade'
                
                    //sh 'terraform taint aws_db_instance.qa_replica3'
                
                    //sh 'terraform taint aws_db_instance.qa_replica2'
                
                    //sh 'terraform apply --auto-approve'
                }
            }
        }
    }
}   
