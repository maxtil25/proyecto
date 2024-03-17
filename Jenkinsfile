pipeline {
    agent any

    stages {
        stage('Ejecutar OWASP ZAP') {
            steps {
                script {
                    // Ejecutar el análisis de ZAP contra el sitio web local
                    sh 'docker exec owasp-zap zap-baseline.py -t http://172.20.0.3/responsive-halloween-website/ -J /zap/report.json'
                }
            }
        }

        stage('Publicar informe de OWASP ZAP') {
            steps {
                // Archivar el informe de OWASP ZAP
                archiveArtifacts artifacts: 'zap/report.json', onlyIfSuccessful: false

                // Publicar el informe como un artefacto Jenkins
                publishHTML(reportDir: 'zap', reportFiles: 'report.json', reportName: 'OWASP ZAP Report', keepAll: true, alwaysLinkToLastBuild: false, allowMissing: false)
            }
        }
    }
}
