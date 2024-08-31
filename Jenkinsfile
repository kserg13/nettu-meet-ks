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
                    apk add --no-cache python3 py3-pip py3-virtualenv
                    python3 -m venv myvenv
                    . myvenv/bin/activate
                    pip install semgrep
                    semgrep --config=auto . --json > semgrep.json
                '''
                archiveArtifacts artifacts: 'semgrep.json', allowEmptyArchive: true
          }
        }
        
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
                //             pwd
                //             ls -l
                //             find . -name "*.json"
                //             '''
                //       archiveArtifacts allowEmptyArchive: true, artifacts: 'test/trivyout.json', caseSensitive: false, defaultExcludes: false, followSymlinks: false
                //     }
                // }

        
                // stage('DT') {
                //     steps {
                //         script {
                //             sh '''
                //             curl -sSfL https://raw.githubusercontent.com/anchore/syft/main/install.sh | sh -s -- -b /usr/local/bin
                //             syft dir:$(pwd) -o cyclonedx-json > sbom.json
                //             '''
                //             sh '''
                //                 curl -k -X 'PUT' 'https://s410-exam.cyber-ed.space:8081/api/v1/project' \
                //                      -H 'accept: application/json' \
                //                      -H 'X-API-Key: odt_SfCq7Csub3peq7Y6lSlQy5Ngp9sSYpJl' \
                //                      -H 'Content-Type: application/json' \
                //                      -d '{
                //                            "name": "kanivets_s",
                //                            "version": "1.0.0",
                //                            "description": "exam-project"
                //                          }'
                //                 '''
                //             sh '''
                //                 curl -k -X 'POST' 'https://s410-exam.cyber-ed.space:8081/api/v1/bom' \
                //                 -H 'accept: application/json' \
                //                 -H 'Content-Type: multipart/form-data'\
                //                 -H 'X-API-Key: odt_SfCq7Csub3peq7Y6lSlQy5Ngp9sSYpJl' \
                //                 -F 'projectName=kanivets_s' \
                //                 -F 'projectVersion=1.0.0' \
                //                 -F 'project=bd056b21-93ad-447e-ba6d-f1104daedfcd' \
                //                 -F 'bom=@sbom.json'
                //                 '''
                //             sh '''
                //                 curl -k -X 'GET' 'https://s410-exam.cyber-ed.space:8081/api/v1/finding/project/bd056b21-93ad-447e-ba6d-f1104daedfcd' \
                //                 -H 'accept: application/json' \
                //                 -H 'X-API-Key: odt_SfCq7Csub3peq7Y6lSlQy5Ngp9sSYpJl' \
                //                 -H 'Content-Type: application/json' \
                //                 -o vulners.json
                //                 '''
                //             archiveArtifacts artifacts: 'sbom.json', allowEmptyArchive: true
                //             archiveArtifacts artifacts: 'vulners.json', allowEmptyArchive: true
                //         }
                //     }
                // }
               
        
                stage('VM') {
                    steps {
                        script {
                            sh '''
                                curl --insecure -X 'POST' \
                                    'https://s410-exam.cyber-ed.space:8083/api/v2/import-scan/' \
                                    -H 'accept: application/json' \
                                    -H 'Authorization: Token c5b50032ffd2e0aa02e2ff56ac23f0e350af75b4' \
                                    -H 'Content-Type: multipart/form-data' \
                                    -F 'active=true' \
                                    -F 'verified=true' \
                                    -F 'minimum_severity=Info' \
                                    -F 'product_name=skanivets' \
                                    -F 'file=@semgrep.json;type=application/json' \
                                    -F 'auto_create_context=true' \
                                    -F 'scan_type=Semgrep JSON Report' \
                               '''
                        }
                    }
                }

                // stage('VM2') {
                //     steps {
                //         script {
                //             sh '''
                //             curl -X 'POST' -kL 'https://s410-exam.cyber-ed.space:8083/api/v2/import-scan/' -H 'accept: application/json' -H 'X-CSRFTOKEN: xlKPcsKGE3OcopuNWpTOKtfzLIS06FRrKbeiG7FMzOjnVU8tiGWJdmqGewocICl1' -H 'Authorization: Token c5b50032ffd2e0aa02e2ff56ac23f0e350af75b4' -H 'Content-Type: multipart/form-data' -F 'active=true' -F 'verified=true' -F'deduplication_on_engagement=true' -F 'minimum_severity=Medium' -F 'scan_date=2024-08-31' -F 'engagement_end_date=2024-08-31' -F 'group_by=component_name' -F 'tags=' -F 'product_name=ks13' -F 'file=@semgrep.json;type=application/json' -F 'auto_create_context=true' -F 'scan_type=Semgrep JSON Report' -F 'engagement=113'
                //             '''
                //         }
                //     }
                // }

        
    }
}
