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
                // stage('trivy') {
                //     agent { label 'dind' }
                //     steps {
                //         sh '''
                //             mkdir report/
                //             docker pull aquasec/trivy:latest
                //             docker run -v ./test:/test aquasec/trivy repo https://github.com/kserg13/nettu-meet-ks -f json -o /test/trivyout.json
                //             docker run --rm -v $(pwd):/test aquasec/trivy repo https://github.com/kserg13/nettu-meet-ks -f json -o /test/trivyout.json
                //             pwd
                //             ls -l
                //             find . -name "*.json"
                //             '''
                //       archiveArtifacts allowEmptyArchive: true, artifacts: 'test/trivyout.json', caseSensitive: false, defaultExcludes: false, followSymlinks: false
                //     }
                // }
                stage('DT') {
                    steps {
                        script {
                            sh '''
                            curl -sSfL https://raw.githubusercontent.com/anchore/syft/main/install.sh | sh -s -- -b /usr/local/bin
                            syft dir:$(pwd) -o cyclonedx-json > sbom.json
                            '''
                            sh '''
                                curl -k -X 'PUT' 'https://s410-exam.cyber-ed.space:8081/api/v1/project' \
                                     -H 'accept: application/json' \
                                     -H 'X-API-Key: odt_SfCq7Csub3peq7Y6lSlQy5Ngp9sSYpJl' \
                                     -H 'Content-Type: application/json' \
                                     -d '{
                                           "name": "kanivets_s",
                                           "version": "1.0.0'",
                                           "description": "exam-project"
                                         }'
                                '''
                            // sh '''
                            //     curl -k -X 'PUT' 'https://s410-exam.cyber-ed.space:8081/api/v1/bom' \
                            //     -H 'Content-Type: application/json'\
                            //     -H 'X-API-Key: odt_SfCq7Csub3peq7Y6lSlQy5Ngp9sSYpJl' \
                            //     -d @sbom.json
                            //     '''
                            archiveArtifacts artifacts: 'sbom.json', allowEmptyArchive: true
                        }
                    }
                }

                           
    }
}
