pipeline {
    agent any
    
    stages {
        stage('Análisis de dependencias con OWASP Dependency-Check') {
            steps {
                script {
                    // Obtener la dirección IP del contenedor de Nginx
                    def nginxContainerIP = sh(script: "docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' nginx", returnStdout: true).trim()
                    
                    // Ejecutar el análisis de dependencias con OWASP Dependency-Check
                    sh "docker run --rm -v $PWD:/src --workdir /src owasp/dependency-check --scan . --out . --format ALL"
                    
                    // Publicar el informe de Dependency-Check
                    dependencyCheckPublisher pattern: 'dependency-check-report.xml'
                }
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
        }
        failure {
            // Acciones adicionales si el pipeline falla
            echo 'El pipeline falló'
        }
    }
}
