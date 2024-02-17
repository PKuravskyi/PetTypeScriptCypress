pipeline {
    agent any
		
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run tests') {
            matrix {
                axes {
                    axis {
                        name 'CONTAINER'
                        values '1', '2', '3', '4', '5'
                    }
                }
                stages {
                    stage('Run tests in container') {
                        steps {
                            script {
                                echo "Running tests in container ${CONTAINER}"
                                sh '''
                                    chmod +x './ShoppingStoreApp/shopping-store-linux-amd64'
                                    ./ShoppingStoreApp/shopping-store-linux-amd64 &
                                '''
                                sh "npm run cy:run"
                            }
                        }
                    }
                }
            }
        }

    }
}
