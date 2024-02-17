pipeline {
	agent any

	tools {
		nodejs '20.11.1'
	}
		
    parameters {
		choice(name: 'TestType', choices: ['smoke', 'ui', 'api'], description: 'Select type of test')
	}

    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main', url: 'https://github.com/PKuravskyi/PetTypeScriptCypress.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh '''
					apt-get install libgtk2.0-0 libgtk-3-0 \
						libgbm-dev libnotify-dev libnss3 \
						libxss1 libasound2 libxtst6 xauth xvfb
					npm install
				'''
            }
        }

        stage('Run tests') {
			steps {
				script {
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
