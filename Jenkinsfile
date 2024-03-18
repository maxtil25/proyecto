pipeline {
    agent any
    
    environment {
        DOCKER_HOME = tool 'docker'
        PATH = "$DOCKER_HOME:$PATH"
    }
    
    stages {
        stage('Instalar Docker') {
            steps {
                script {
                    def dockerVersion = sh(script: 'docker --version', returnStdout: true).trim()
                    echo "Versión de Docker instalada: ${dockerVersion}"
                }
            }
        }
        
        stage('Verificar Docker ps') {
            steps {
                script {
                    def dockerOutput = sh(script: 'docker ps', returnStdout: true).trim()
                    echo "Salida del comando 'docker ps': ${dockerOutput}"
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    def nodeVersion = sh(script: 'node --version', returnStdout: true).trim()
                    echo "Versión de Node.js en el contenedor: ${nodeVersion}"
                }
            }
        }
    }
}
