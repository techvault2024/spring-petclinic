pipeline {
    agent any
    
    stages {
        stage("build"){
            steps {
                sh "./mvnw package"
            }
        }
        stage("capture"){
            steps {
                archiveArtifacts '**/target/*.jar'
                junit stdioRetention: '', testResults: '**/target/surefire-reports/TEST*.xml'
                jacoco()
            }
        }
    }
    post {
        always {
            emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}",
                to: 'always@foo.com',
                recipientProviders: [previous()],
                subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]"
        }
        
    }
}    