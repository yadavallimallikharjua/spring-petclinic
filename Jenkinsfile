pipeline {
    agent any
    environment {
        registry = "9492453554/myimage0"
        registryCredential = 'DOCKER_HUB'
        dockerImage = ''
    }
    stages {
        stage('scm') {
            steps {
                git branch: 'development', url: 'https://github.com/yadavallimallikharjua/spring-petclinic.git'
            }
        }
        stage('Build image') {
            steps {
                script {
                    dockerImage = docker.build registry 
                }
            }
        }
        stage('push our image') { 
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy App') {
            steps {
                script {
                kubernetesDeploy(configs: "myimage0.yaml", kubeconfigId: "k8_config")
                }
            }
        }
    }
}