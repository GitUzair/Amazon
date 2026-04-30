pipeline {
    agent any
    
    stages {
        stage('Checkout Code') {
            steps {
                // Pull the code from the GitHub repository
                git url: 'https://github.com/GitUzair/Amazon', branch: 'master'  // Use the desired branch
            }
        }

        stage('Build') {
            steps {
                    echo "Building the project..."
                    sh 'cd Amazon && mvn clean install'
            }
        }
    }
    post {
        always {
            script {
                def buildStatus = currentBuild.result ?: 'SUCCESS'
                def slackWebhookUrl = 'https://hooks.slack.com/services/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'
                def message = """
                {
                    "text": "Jenkins Build Status: ${buildStatus}",
                    "attachments": [
                        {
                            "text": "Build ${buildStatus}",
                            "color": "${buildStatus == 'SUCCESS' ? 'good' : 'danger'}"
                        }
                    ]
                }
                """
                sh """
                curl -X POST -H 'Content-type: application/json' --data '${message}' ${slackWebhookUrl}
                """
            }
        }
    }
}
