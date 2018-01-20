node('php'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }
    
    stage('Fetch') {
        checkout scm
    }
    
    stage('Build'){
        sh 'composer install --no-scripts --prefer-dist --no-dev --ignore-platform-reqs'
    }
    
    stage('config') {
        parallel(
            'config cache': {
                echo 'Tarefa de configuracao'
            },
            'config route': {
                echo 'Segunda parte da configuracao'
            }
        )
    }
    stage('Docker Build') {
        sh 'docker build -t cromado/todoapi:$BUILD_NUMBER .'
    }
    
    stage('Docker Ship') {
        sh 'docker push cromado/todoapi:$BUILD_NUMBER'
    }
}
