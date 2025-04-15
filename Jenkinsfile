pipeline {
    agent {
        docker {
            image 'python:3.10'
            args '-u root'
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
                    echo "Kiểm tra môi trường..."
                    python3 --version
                    pip3 --version
                    ls -la
                    if [ ! -f requirements.txt ]; then
                        echo "LỖI: Không tìm thấy requirements.txt"
                        exit 1
                    fi
                    if [ ! -f app.py ]; then
                        echo "LỖI: Không tìm thấy app.py"
                        exit 1
                    fi
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --no-cache-dir -r requirements.txt
                '''
            }
        }
        stage('Test Streamlit app') {
            steps {
                sh '''
                    . venv/bin/activate
                    streamlit --version
                    python3 -c "import streamlit; print('Streamlit imported successfully')"
                '''
            }
        }
    }
}