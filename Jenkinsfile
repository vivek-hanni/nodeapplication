pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', credentialsId: 'vivek-hanni2demo', url: 'https://github.com/vivek-hanni/nodeapplication.git'
            }
        }
        stage('IMAGE') {
            steps {
                bat 'docker build -t hannidocker/nodeapp:1.1 .'
            }
        }
        stage('Docker Push Hub') {
           steps {
              withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerhubpwd')]) {
                  bat 'docker login -u hannidocker -p %dockerhubpwd%'
                  bat 'docker push hannidocker/nodeapp:1.1'
              }
            }
        }

    }
}
