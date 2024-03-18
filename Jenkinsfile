pipeline {
    agent any
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/maxtil25/proyecto.git'
            }
        }
        
        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '--scan target/', odcInstallation: 'owasp-dc'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        
        stage('Montar proyecto en nginx 11') {
            steps {
                // Crea el directorio si no existe
                sh "mkdir -p /usr/share/nginx/html/prueba"
                
                // Copia los archivos HTML, CSS, JavaScript al servidor web
                sh "cp -r * /usr/share/nginx/html/ "
            }
        }
    }
}
