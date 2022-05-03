pipeline {
   agent any

   stages {

       stage('codigo') {
           steps{
               git 'https://github.com/marlyngiselle/web-astronauta-dockerfile'
           }
       }

       stage('build') {
           steps {
                sh 'docker stop elonmusk'
                sh 'docker rm elonmusk'
                sh 'docker build -t mgiselle/${JOB_NAME}:v${BUILD_NUMBER} .'
           }
       }

       stage('test') {
           steps {
               echo "Ingresa a la pagina http://neoastronauta"
           }
       }

       stage('release') {
           steps {
                sh 'docker tag mgiselle/${JOB_NAME}:v${BUILD_NUMBER} mgiselle/${JOB_NAME}:latest'
                sh 'docker login -u="mgiselle" -p="Tasia.2411"'
                sh 'docker push mgiselle/${JOB_NAME}:v${BUILD_NUMBER}'
                sh 'docker push mgiselle/${JOB_NAME}:latest'
                sh 'docker rmi mgiselle/${JOB_NAME}:v${BUILD_NUMBER}'
                sh 'docker rmi mgiselle/${JOB_NAME}:latest'
           }
       }

       stage('deploy') {
           steps {
                sh 'docker run -d -p 80:80 --name elonmusk mgiselle/${JOB_NAME}:latest'
           }
       }
   }
   

}