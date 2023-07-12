pipeline {
    agent none 
    stages {
        stage('Build') { 
            agent {
                docker {
                    image 'python:2-alpine' 
                }
            }
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py' 
            }
          }
        stage('Test') {
            agent {
                docker {
                    image 'qnib/pytest'
                }
            }
            steps {
                sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
          }
        stage('Deliver') {
            steps {
                sh 'echo "run command pyinstaller --onefile sources/add2vals.py "'
                sh 'echo "docker env infos"'
                sh 'whoami && id && groups && ls -l /root/.bashrc'
            }
        }
    }
}
