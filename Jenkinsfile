pipeline {
    agent any
    
    stages {
        stage('Obtención de código fuente') {
            steps {
                git branch: 'main', url: 'https://github.com/maxtil25/proyecto.git'
            }
        }
        
        stage('Análisis de dependencias con OWASP Dependency-Check') {
            steps {
                dependencyCheck additionalArguments: ''' 
                    -o './'
                    -s './'
                    -f 'ALL' 
                    --prettyPrint''', odcInstallation: 'owasp-d'
                
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
        
        stage('Despliegue en Nginx 1') {
            steps {
                // Crea el directorio si no existe
                sh "mkdir -p /usr/share/nginx/html/prueba2"
                
                // Copia los archivos HTML, CSS, JavaScript al servidor web
                sh "cp -r * /usr/share/nginx/html/prueba2"
            }
        }
    }
    
}
