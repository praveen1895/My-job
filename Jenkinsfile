pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }
    post {
        always {
            script {
                def ghEvent = env.GITHUB_EVENT_NAME
                def ghPayload = readJSON file: env.GITHUB_EVENT_PATH
                
                if (ghEvent == 'issues' || ghEvent == 'issue_comment') {
                    // Trigger the build if a new issue is created or a comment is added to an existing issue
                    echo 'New issue or issue comment detected. Triggering build...'
                    build job: 'my-job'
                }
                else if (ghEvent == 'push') {
                    // Trigger the build if a new commit is pushed to the repository
                    echo 'New commit detected. Triggering build...'
                    build job: 'my-job'
                }
            }
        }
    }
}
