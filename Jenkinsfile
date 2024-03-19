

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
        stage('Despliegue en Nginx') {
            steps {
                // Comprobación de la existencia de la carpeta "prueba2"
                sh "ls -l /usr/share/nginx/html"
                
                // Crea el directorio si no existe
                sh "mkdir -p /usr/share/nginx/html/prueba2"
                
                // Comprobación después de la creación de la carpeta "prueba2"
                sh "ls -l /usr/share/nginx/html"
                
                // Copia los archivos del directorio de trabajo del pipeline al directorio de Nginx
                sh "cp -r ${WORKSPACE}/* /usr/share/nginx/html/prueba2"
            }
        }
    }
    
    post {
        always {
            // Acciones de limpieza
            deleteDir() // Elimina el directorio de trabajo del Jenkins
        }
        success {
            // Acciones adicionales si el pipeline tiene éxito
            echo 'El pipeline se ejecutó correctamente'
            // Puedes agregar aquí notificaciones por correo electrónico, por ejemplo
        }
        failure {
            // Acciones adicionales si el pipeline falla
            echo 'El pipeline falló'
            // Puedes agregar aquí notificaciones por correo electrónico, por ejemplo
        }
    }
}
