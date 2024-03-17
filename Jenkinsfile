pipeline {
    agent any
    
    parameters {
        string(name: 'application_url', defaultValue: 'http://localhost:80', description: 'URL for ZAP attack')
    }
    
    stages {
        stage('Setup') {
            steps {
                script {
                    if (params.application_url == 'http://localhost:80') {
                        sh "sudo docker run --rm --name vulnerable_app -d -p 80:80 vulnerables/web-dvwa"
                    } else {
                        echo "Skipping setup stage as application_url is not 'http://localhost:80'"
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                dir('/home/ec2-user/ZAP_2.9.0') {
                    sh "./zap.sh -quickurl ${params.application_url} -quickprogress -quickout ${WORKSPACE}/report.xml -cmd"
                }
            }
        }
        
        stage('Cleanup') {
            steps {
                script {
                    if (params.application_url == 'http://localhost:80') {
                        sh "sudo docker stop vulnerable_app"
                    } else {
                        echo "Skipping cleanup stage as application_url is not 'http://localhost:80'"
                    }
                }
            }
        }
    }
    
    post {
        success {
            archiveArtifacts artifacts: 'report.xml', fingerprint: true
            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: false,
                reportDir: '',
                keepAll: true,
                reportFiles: 'report.xml',
                reportName: "ZAP Report"
            ])
        }
    }
}
