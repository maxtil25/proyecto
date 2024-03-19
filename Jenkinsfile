pipeline {
    agent any
    
    stages {
        stage('Obtención de código fuente') {
            steps {
                git branch: 'main', url: 'https://github.com/maxtil25/proyecto.git'
            }
        }
        
        stage('Despliegue en Nginx') {
            steps {
                // Crea el directorio si no existe
                sh "mkdir -p /usr/share/nginx/html"
                
                // Copia todo el contenido del repositorio al directorio de Nginx
                sh "cp -r proyecto/* /usr/share/nginx/html"
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
