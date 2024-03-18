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
        
        stage('Montar proyecto en nginx 10') {
            steps {
                // Copia los archivos HTML, CSS, JavaScript al servidor web
                sh "cp -r * /usr/share/nginx/html/responsive-halloween-website "
            }
        }
    }
}
