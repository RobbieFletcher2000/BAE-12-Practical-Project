pipeline {
    agent any 
    environment {
        USER_NAME = credentials('USER')
        PASSWORD = credentials('PASSWORD')
        DB_URI = credentials('DB_URI')
        S_KEY = credentials('S_KEY')

    }
    stages{
        stage('build'){
            steps{
                sh 'echo "This is the build stage"'
                sh 'pwd && ls'
                sh 'docker-compose build'
            }
        }
        stage('test'){
            steps{
                sh 'pip3 install -r ./backend/requirements.txt'
                sh 'cd backend && python3 -m pytest'


                sh 'pip3 install -r ./frontend/requirements.txt'
                sh 'cd frontend && python3 -m pytest'

            }
        }
        stage('push'){
            steps{
                sh 'echo "This is the push stage"'
                sh 'docker login -u ${USER_NAME} -p ${PASSWORD} && docker-compose push'
            }    
        }
        stage('deploy'){
            steps{
                sh 'echo "This is the deploy stage"'
                sh 'docker stack deploy --compose-file docker-compose.yaml flask-stack'
            
            }
        
        }
        
    }
}
