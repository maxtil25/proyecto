pipeline {
    agent any
    
    stages {
        stage('Verificar Docker') {
            steps {
                script {
                    def dockerOutput = sh(script: 'docker --version', returnStdout: true).trim()
                    echo "Salida del comando Docker: ${dockerOutput}"
                }
            }
        }
    }
}
