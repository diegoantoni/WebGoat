pipeline{
    agent any
    environment {
        NAME_APP = "webgoat"
        PORT_APP = "3333"
        DIR_DOCKER = "/home/jenkins/workspace/pipeline-webgoat/docker/"
    }
    
    stages {
        stage('Build da imagem'){
            agent { node 'teste' }
            steps {
                git url: 'https://github.com/diegoantoni/WebGoat'
                script {
                    sh '''
                    cd $DIR_DOCKER
                    '''
                    docker.build "$NAME_APP:latest"
                }
            }
        }
        
        stage('Executando Container'){
            agent { node 'teste' }
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



