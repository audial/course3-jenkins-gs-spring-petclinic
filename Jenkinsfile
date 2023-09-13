pipeline {
    agent any
    
    stages {
        stage("Build") {
            steps {
                sh "./mvnw package"
            }
        }
        stage("Capture") {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar'
                jacoco()
            }
        }
    }
    post {
        always {
                emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}", recipientProviders: [developers()], subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]", to: 'always@foo.bar'
        }
    }
}
