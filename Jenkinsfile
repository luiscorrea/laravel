node('php7'){
    stage('Clean'){
        deleteDir()
      
    }

    stage('Fetch') {
        checkout scm
    }

    stage('Docker Build') {
        sh 'sudo docker build -t luiscorrea/laravel:$BRANCH_NAME-$BUILD_NUMBER .'
    }

    stage('Docker Ship') {
        sh 'sudo docker push luiscorrea/laravel:$BRANCH_NAME-$BUILD_NUMBER'
    }
    
    stage('Docker Clean') {
        sh 'sudo docker rmi -f luiscorrea/laravel:$BRANCH_NAME-$BUILD_NUMBER'
    }
}
