pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                git branch: 'main', url: 'https://github.com/maxtil25/proyecto.git'
            }
        }
        stage('Verificacion Dependencia') {
            steps {
                dependencyCheck additionalArguments: '--format HTML', odcInstallation: 'owasp-dc'
            }
        }
    }
}
