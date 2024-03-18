pipeline {
    agent any
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/jaiswaladi246/Petclinic.git'
            }
        }
        
        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '--scan target/', odcInstallation: 'owasp-dc'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        
        stage('Montar proyecto en nginx 7') {
            steps {
                // Crea el directorio si no existe
                sh "mkdir -p /usr/share/nginx/html/proyecto2"
                
                // Copia los archivos HTML, CSS, JavaScript al servidor web
                sh "cp -r * /usr/share/nginx/html/proyecto2 "
            }
        }
    }
}
