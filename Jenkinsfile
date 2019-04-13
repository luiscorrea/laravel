node('php7'){
    stage('Clean'){
        deleteDir()
    }

    stage('Fetch') {
        checkout scm
    }

    stage('Build for Tests'){
        sh 'composer install --no-scripts --prefer-dist --ignore-platform-reqs'
    }

    stage('config') {
        parallel(
            'Copy .env file': {
                echo 'cp .env.example .env'
            },
            'config route': {
                echo 'Tarefa Paralela 02'
            }
        )
    }

    //stage('Tests') {
    //    sh 'php ./vendor/bin/phpunit'
    //}

    stage('Build'){
        sh 'composer install --no-scripts --prefer-dist --no-dev --ignore-platform-reqs'
    }

    stage('Docker Build') {
        sh 'sudo docker build -t luiscorrea/laravel:$BRANCH_NAME-$BUILD_NUMBER .'
    }

    stage('Docker Ship') {
        sh 'sudo docker push luiscorrea/laravel:$BRANCH_NAME-$BUILD_NUMBER'
    }
    
    stage('Docker Cleanup') {
        sh 'sudo docker rmi -f luiscorrea/laravel:$BRANCH_NAME-$BUILD_NUMBER'
    }
}
