pipeline{
    agent any
    tools{
        maven 'maven_3_8_7'
    }
    stages{
        stage('CompileandRunSonarAnalysis'){
            
            steps{
               withCredentials([string(credentialsId: 'sonarqube', variable: 'sonarqube')]) {
                   sh 'mvn clean package sonar:sonar -Dsonar.login=$sonarqube -Dsonar.host.url=https://sonarcloud.io -Dsonar.projectKey=sonarqubeapp -Dsonar.organization=sonarqubeapp'
                
               }
            }
        }

        // build docker image
        stage('Build Docker Image'){
            steps{
            withDockerRegistry([credentialsId: "dockerlogin", url:""]){
                script{
                   app =  docker.build('myjavaapp:$(env.BUILD_NUMBER)')
                 
                }
            }
            }
        }

        // push docker image
        stage('Push Docker Image to amazon ecr'){
            steps{
            script{

                // docker.withRegistry('https://registry.hub.docker.com', 'dockerlogin'){


                docker.withRegistry('https://949335805735.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:aws-credentials'){
  
                    app.push("1.0.1")
                }
            }
        }

        }

        // stage('kubernetes deployment'){
        //     steps{
        //         withKubeConfig([credentialsId: 'kubelogin']){
        //             sh('kubectl delete all -n devsecops')
        //             sh ('kubectl apply -f deployment.yaml --namespace=devsecops')
        //         }
        //     }
            
        // }
    }
}
