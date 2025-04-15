pipeline {
    agent any

    environment {
        STREAMLIT_PORT = '8501'
    }

    stages {
        stage('Clone source') {
            steps {
                git 'https://github.com/Nguyenbaothanh/OCR-Jenkins.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'pip install -r requirements.txt --user'
            }
        }

        stage('Run Streamlit app') {
            steps {
                // Dừng streamlit cũ nếu có
                sh 'pkill -f streamlit || true'

                // Chạy lại app trong nền
                sh 'nohup python -m streamlit run app.py --server.port=$STREAMLIT_PORT &'
            }
        }
    }
}
