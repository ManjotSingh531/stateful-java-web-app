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
        stage('Deploy Application in Staging Environment') {
            steps {
                build job: 'Deploy tomcat application to staging env'
            }
        }
    }
}
