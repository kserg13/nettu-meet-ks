pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        // stage('semgrep') {
        //     agent { label 'alpine' } 
        //     steps {
        //         sh '''
        //             apk add --no-cache python3 py3-pip py3-virtualenv
        //             python3 -m venv myvenv
        //             . myvenv/bin/activate
        //             pip install semgrep
        //             semgrep --config=auto . --json > k-semgrep.json
        //         '''
        //         archiveArtifacts artifacts: 'k-semgrep.json', allowEmptyArchive: true
        //   }
        // }
            stage('semgrep') {
                agent { label 'alpine' } 
                steps {
                    sh '''
                        zap.sh -suppinfo
                    '''
                    // archiveArtifacts artifacts: 'zapout.json', allowEmptyArchive: true, caseSensitive: false, defaultExcludes: false, followSymlinks: false
                }
            }
    }
}
