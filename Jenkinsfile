pipeline {
    agent any
    
    
    parameters{
        
            choice(choices: ["innovation", "lyceum"], description: 'aws profile selection', name: 'awsProfile')
            choice(choices: ["us-east-1", "us-west-2", "eu-central-1"], description: 'aws region', name: 'awsRegion')
            string(defaultValue: 'hp-altuscare', description: 'db identifier', name: 'dbId')
    }

    stages {
        stage('Checkout') {
            steps {
                 script{
                        
                          git branch: "master", credentialsId: "git", url: "https://github.com/area9innovation/expose.git"
                        
                    }
                }
            }
        
        stage('Create snapshot') {
            steps {
                script {
                
                    println("AWS Profile used is " + params.awsProfile)
                    
                    withCredentials([[
                        $class: 'AmazonWebServicesCredentialsBinding', 
                        accessKeyVariable: 'AWS_ACCESS_KEY_ID', 
                        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY',
                        credentialsId: "${params.awsProfile}"
                    ]]) {
                        def snapshotId = 'for-qa-' + new Date().format('yyyy-MM-dd')
                    
                        //sh "aws rds create-db-snapshot --db-snapshot-identifier '$snapshotId' --db-instance-identifier '$params.dbId' --region '$params.awsRegion'"
                        
                        //def snapshotId = sh(script: "python3 snapshot.py '$params.awsRegion' '$params.dbId'",returnStdout: true)
                        
                     
                    }
                }  
                
            }
        }
        stage('Upgrade QA DB from the latest snapshot') {
            steps {
                script {
                    sleep(time: 30, unit: "SECONDS")
                
                    withCredentials([[
                        $class: 'AmazonWebServicesCredentialsBinding', 
                        accessKeyVariable: 'AWS_ACCESS_KEY_ID', 
                        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY',
                        credentialsId: "${params.awsProfile}"
                    ]]) {
                        sh 'cd infra/lyceum/qa/db'
                        sh 'terraform init -upgrade'
                        sh 'terraform plan'
                        
                        
                        //sh 'terraform init -upgrade'
                
                        //sh 'terraform taint aws_db_instance.qa_replica3'
                
                        //sh 'terraform taint aws_db_instance.qa_replica2'
                
                        //sh 'terraform apply --auto-approve'
                    }   
                }
            }
        }
    }
}   
