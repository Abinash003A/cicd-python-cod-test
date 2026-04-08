#install these maually 1st
sudo yum install -y git python3 python3-pip

## Pipeline code
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
        git branch: 'main', url: 'https://github.com/Abinash003A/cicd-python-cod-test.git'
            }
        }

        stage('Test') {
            steps {
                sh '''
                python3 -m venv venv
                source venv/bin/activate
                pip install -r requirements.txt
                pytest
                '''
            }
        }
stage('Run App') {
    steps {
        sh '''
        source venv/bin/activate

        nohup python3 app.py > app.log 2>&1 &
        '''
    }
}
    }
}
