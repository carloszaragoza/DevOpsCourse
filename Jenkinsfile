pipeline {
    agent any
    tools {
        maven 'M3'
        jdk 'jdk10'
    }
    stages {
        stage('Build Frontend Web') {
            steps {
                echo 'Building Frontend Angular'
                dir ('Angular6BaseCli/'){
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
        stage('Deploy Frontend Web') {
            steps {
                echo 'Deploy Frontend Angular'
                sh 'docker build -t front1 .'
                sh 'docker run -d -p 9090:80 front1 '
            }
        }
    }
    post { 
        always { 
            deleteDir()
        }
        success {
            echo 'I succeeeded!'
        }
        unstable {
            sh 'docker-compose down'
            echo 'I am unstable :/'
        }
        failure {
            sh 'docker-compose down'
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }
}