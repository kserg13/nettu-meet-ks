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
                    // apk add --no-cache python3 py3-pip
                    // python3 -m venv myvenv
                    // . myvenv/bin/activate
                    pip install semgrep
                    semgrep --config=auto . --json > k-semgrep.json
                '''
                archiveArtifacts artifacts: 'k-semgrep.json', allowEmptyArchive: true
          }
        }
    }
}
