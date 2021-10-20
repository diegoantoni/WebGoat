pipeline{
    agent any
    environment {
        NAME_APP = "webgoat"
        PORT_APP = "3333"
    }
    
    stages {
        stage('Build da imagem'){
            agent { node 'master' }
            steps {
                git url: 'https://github.com/diegoantoni/WebGoat'
                script {
                    docker.build "$NAME_APP:latest"
                }
            }
        }

        stage('Clone do Codigo'){
            steps{
                git url: 'https://github.com/diegoantoni/WebGoat'
            }
        }
        
        stage('Executando Container'){
            agent { node 'master' }
            steps {
                sh '''
                    if [ ! "$(curl -s localhost:$PORT_APP &> /dev/null)" ]; then
                    docker run -d --name $NAME_APP -p $PORT_APP:3333 $NAME_APP:latest
                    fi
                '''
            } 
        }

    }

}

