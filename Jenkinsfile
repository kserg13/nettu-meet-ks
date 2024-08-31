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
        
            // stage('zap') {
            //     agent { label 'alpine' } 
            //     steps {
            //         sh '''
            //             apk add --no-cache openjdk11-jre-headless wget unzip
            //             wget https://github.com/zaproxy/zaproxy/releases/download/w2024-08-27/ZAP_WEEKLY_D-2024-08-27.zip
            //             unzip ZAP_WEEKLY_D-2024-08-27.zip -d zap
            //             pwd
            //             zap/ZAP_D-2024-08-27/zap.sh -cmd -quickurl https://s410-exam.cyber-ed.space:8084 -quickout /home/jenkins/workspace/skanivets_exam/zapout.json
            //             pwd
            //             ls -l
            //             find . -name "*.json"
            //             '''
            //         archiveArtifacts allowEmptyArchive: true, artifacts: 'zapout.json'
            //     }
            // }
                stage('trivy') {
                    agent { label 'dind' }
                    steps {
                        sh '''
                            docker run aquasec/trivy --format json --output /report/trivyout.json repo https://github.com/kserg13/nettu-meet-ks
                            pwd
                            ls -l
                            find . -name "*.json"
                            '''
                        archiveArtifacts allowEmptyArchive: true, artifacts: '/report/trivyout.json'
                    }
                }
                            
    }
}
