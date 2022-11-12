pipeline {
    agent any
    
    stages {
        stage ('OWASP Dependency-Check Vulnerabilities') {
            agent {
                docker {
                    image "owasp/dependency-check:latest"
                    args "--volume '/opt/jenkins/dependency-check-data:/usr/share/dependency-check/data' --entrypoint="
                }
            }
            
            steps {
                echo "[-] Running OWASP Dependency Check"
                
                sh '''
                /usr/share/dependency-check/bin/dependency-check.sh \
                --enableExperimental \
                --format XML \
                --out dependency-check-report.xml \
                --project "Lab6" \
                --scan .
                '''

                echo "[-] End of OWASP Dependency Check"
            }

            post {
                always {
                    dependencyCheckPublisher (pattern: 'dependency-check-report.xml')
                }
            }
        }
    }
}