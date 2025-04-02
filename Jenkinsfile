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

        // // build docker image
        // stage('BuildDockerImage'){
        //     steps{
        //     withDockerRegistry([credentialsId: "dockerlogin", url:""]){
        //         script{
        //            app =  docker.build("tech365app")
                 
        //         }
        //     }
        //     }
        // }

        // // push docker image
        // stage('PushDockerImage'){
        //     steps{
        //     script{

        //         // docker.withRegistry('https://registry.hub.docker.com', 'dockerlogin'){


        //         docker.withRegistry('https://222634367210.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:aws-credentials'){
  
        //             app.push("latest")
        //         }
        //     }
        // }

        // }

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
