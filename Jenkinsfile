pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test'){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps {
                echo 'Test stage'
                sh '[ -f build/index.html ]'
                sh 'ls -l build/index.html'

                sh 'npm test /a'
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
