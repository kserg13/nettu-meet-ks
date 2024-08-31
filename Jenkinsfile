pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('semgrep') {
            steps {
                sh '''
                    pip install semgrep
                    semgrep --config=auto . --json > k-semgrep.json
                '''
                archiveArtifacts artifacts: 'k-semgrep.json', allowEmptyArchive: true
          }
        }
    }
}
