pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archive the build artifacts!'
                    archiveArtifacts artifacts: '**/*.war', fingerprint: true
                }
                failure {
                    echo 'Build failed!'
                }
            }
        }
        stage('Build Tomcat Docker Image') {
            steps {
                sh 'docker build -t mytomcatwebapp:${env.BUILD_NUMBER} .'
            }
        }
    }
}
