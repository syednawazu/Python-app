pipeline {
    
    agent any
    
    environment {
        docker Image ='pythonapp'
        registry = 'sdnawaz/pythonapp'
        registryCredential ='dockerhub'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/syednawazu/Python-app.git']])
            }
        }    
        
        stage('Build Docker image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry

                }
            }
        }

        stage ('Uploading Image') {
            steps {
                script {
                         docker.withRegistry( '', registryCredential ) {
                         dockerImage.push()
                    }     
                }        
            }
        }  
    }    
}
