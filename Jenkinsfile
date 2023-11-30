pipeline {
    agent none

    stages {
        stage('git checkout') {
            agent {
                label 'agent1'
            }
            steps {
                git branch: 'main', credentialsId: 'vivek-hanni2demo', url: 'https://github.com/vivek-hanni/nodeapplication.git'
            }
        }
        stage('IMAGE') {
            agent {
                label 'master'
            steps {
                script {
                    def dockerTag = "1.${env.BUILD_NUMBER}"
                    sh "docker build -t hannidocker/nodeapp:$dockerTag ."
                }
            }
        }
        stage('Docker Push Hub') {
            agent {
                label 'master'
            steps {
                withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u hannidocker -p $dockerhubpwd'
                    script {
                        def dockerTag = "1.${env.BUILD_NUMBER}" 
                        sh "docker push hannidocker/nodeapp:$dockerTag"
                    }
                }
            }
        }
    }
}



// pipeline {
//     agent any

//     stages {
//         stage('git checkout') {
//             steps {
//                 git branch: 'main', credentialsId: 'vivek-hanni2demo', url: 'https://github.com/vivek-hanni/nodeapplication.git'
//             }
//         }
//         stage('IMAGE') {
//             steps {
//                 script {
//                     def dockerTag = "1.${env.BUILD_NUMBER}"
//                     bat "docker build -t hannidocker/nodeapp:$dockerTag ." 
//                 }
//             }
//         }
//         stage('Docker Push Hub') {
//            steps {
//               withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerhubpwd')]) {
//                   bat 'docker login -u hannidocker -p %dockerhubpwd%'
//                   script {
//                       def dockerTag = "1.${env.BUILD_NUMBER}" 
//                       bat "docker push hannidocker/nodeapp:$dockerTag"
//                   }
//               }
//             }
// 			}
//         stage('Deploy to k8s'){
//             steps{
//                 script{
//                     kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'minikubeconfig')
//                 }
//             }
//         }
//    }
// }
