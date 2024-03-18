pipeline {
    agent any
    options {
        skipDefaultCheckout true
    }
    stages {
        stage('Run as root') {
            agent {
                docker {
                    image 'nginx' // Reemplaza esto con el nombre de la imagen de Docker que estás utilizando en tu pipeline
                    args '-u root' // Esto ejecutará el contenedor Docker como usuario root
                }
            }
            steps {
                sh '''
                git clone https://github.com/maxtil25/proyecto.git
                cp -r Dockerfile Jenkinsfile README.md Steps.txt bin dependency-check-report.html dependency-check-report.xml mvnw mvnw.cmd pom.xml src target /usr/share/nginx/html/proyecto2
                '''
            }
        }
        
        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '--scan target/', odcInstallation: 'owasp-dc'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        
        stage('Montar proyecto en nginx 5') {
            steps {
                // Crea el directorio si no existe
                sh "mkdir -p /usr/share/nginx/html/proyecto2"
                
                // Copia los archivos HTML, CSS, JavaScript al servidor web
                sh "cp -r * /usr/share/nginx/html/proyecto2 "
            }
        }
    }
}
