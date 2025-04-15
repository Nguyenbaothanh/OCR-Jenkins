pipeline {
    agent any

    stages {
        stage('Clone source') {
            steps {
                git branch: 'main', url: 'https://github.com/Nguyenbaothanh/OCR-Jenkins.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh '''
                    python -m venv venv
                    source venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Streamlit app') {
            steps {
                sh '''
                    source venv/bin/activate
                    python -m streamlit run app.py
                '''
            }
        }
    }
}
