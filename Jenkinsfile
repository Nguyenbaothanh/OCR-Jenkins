pipeline {
    agent {
        // Use a Docker agent with Python pre-installed
        docker {
            image 'python:3.9'
            args '-u root' // Run as root to avoid permission issues
        }
    }

    environment {
        STREAMLIT_PORT = '8501'
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
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Streamlit app') {
            steps {
                sh '''
                    # Stop any existing Streamlit process (optional, safer alternative)
                    ps aux | grep '[s]treamlit' | awk '{print $2}' | xargs kill -9 || true
                    
                    # Activate virtual environment and run Streamlit
                    . venv/bin/activate
                    nohup python3 -m streamlit run app.py --server.port=$STREAMLIT_PORT &
                '''
            }
        }
    }

    post {
        always {
            // Clean up processes if needed
            sh 'ps aux | grep '[s]treamlit' | awk '{print $2}' | xargs kill -9 || true'
        }
    }
}