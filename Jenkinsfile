pipeline {
    agent {
        docker {
            image 'python:3.9' // Python 3.9 image includes python3, pip, and venv
            args '-u root'     // Run as root to avoid permission issues
        }
    }
    stages {
        stage('Clone source') {
            steps {
                git branch: 'main', url: 'https://github.com/Nguyenbaothanh/OCR-Jenkins.git'
            }
        }
        stage('Install dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }
        stage('Run Streamlit app') {
            steps {
                sh '''
                    . venv/bin/activate
                    python3 -m streamlit run app.py --server.headless true &
                    sleep 10
                    kill %1
                '''
            }
        }
    }
}