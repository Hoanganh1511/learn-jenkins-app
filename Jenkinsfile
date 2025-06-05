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
            steps{
                sh '''
                echo "Test stage"
                find ./build -mindepth 2 -maxdepth 2 -type f -name "index.html"
                if [ $? -eq 0 ]; then
                    echo "index.html found"
                else
                    echo "index.html not found"
                fi

                npm test
                '''
            }
        }
    }
}
