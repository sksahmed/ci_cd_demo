pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                git branch: 'main', url: 'https://github.com/sksahmed/ci_cd_demo.git'
            }
        }

        stage('Docker Stage') {
            steps {

                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASW', usernameVariable: 'UNS')]) {

                sh "echo ${PAWS} | docker login -u ${UNS} --password-stdin"
                } 


                echo 'Docker Process Start'
                sh "docker build -t smarok/project:${BUILD_NUMBER} ."
                sh 'docker images'

                //sh "docker push smarok/project:${BUILD_NUMBER}"

                sh 'docker rmi -f $(docker images -q)'
                echo 'Docker Process Stop'
                
            }
        }
    }
}
