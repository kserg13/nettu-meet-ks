pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('semgrep') {
            agent { label 'alpine' } 
            steps {
                sh '''
                    apk add --no-cache python3 py3-pip
                    pip3 install semgrep
                    semgrep --config=auto . --json > k-semgrep.json
                '''
                archiveArtifacts artifacts: 'k-semgrep.json', allowEmptyArchive: true
          }
        }
    }
}
