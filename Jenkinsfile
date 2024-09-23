pipeline {
    agent any

    environment {
        // Set npm cache directory to a writable path
        NPM_CONFIG_CACHE = "${WORKSPACE}/.npm" 
    }

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
        stage('Test') {
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
                    if [ -e /builds/index.html]
                        then
                            echo "File exists."
                    else 
                        echo "File Doesn't exist."
                    fi
                    npm run test
                    ls -la
                '''
            }
                
    }
}
}    

