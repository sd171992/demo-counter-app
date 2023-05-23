pipeline {
    agent any

    parameters{

        choice(name: 'action', choices: 'create\ndestory\ndestroyekscluster', description: 'Create/update or destroy the eks cluster')
        string(name: 'cluster', defaultValue: 'devopsthehardway-cluster', description: 'Eks cluster name')
        string(name: 'region', defaultValue: 'us-east-1', description: 'Eks cluster region')
    }
    environment{
        ACCESS_KEY = credentials('aws_access_key_id')
        SECRET_KEY = credentials('aws_secret_access_key_id')
    }

    stages{
        
        stage('Git Checkout'){
            steps{
                script{
                    git branch: 'main', url: 'https://github.com/sd171992/demo-counter-app.git'
                }
            }
            stage('eks connect'){
            steps{

                sh """
                
                aws configure set aws_access_key_id "$ACCESS_KEY"
                aws configure set aws_secret_access_key_id "$SECRET_KEY"
                aws configure set region ""
                aws eks --region ${params.region} update-kubeconfig --name ${params.cluster}

                """;


                }
            }
            // stage('eks deployment'){
            //     when { expression { params.action == 'create'}}
            //     steps{

            //         script{

            //             def apply = false
            //             try{

            //                 input message: 'please confirm the apply to initiate the deployment', ok: 'Ready to apply confir'
            //                 apply = true
            //             }
            //             catch(err){
            //                 apply = false
            //                 CurrentBuild.result= 'UNSTABLE'
            //             }
            //             if(apply){

            //                 sh """
            //                 kubectl apply -f .
            //                 """

            //             }
            //         }
            //     }
            // }
        }
    }
}
