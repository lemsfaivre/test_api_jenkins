// Examples of groovy Jenkins files
// https://www.jenkins.io/doc/book/pipeline/docker/
// https://betterprogramming.pub/how-too-add-github-webhook-to-a-jenkins-pipeline-62b0be84e006


pipeline {
    /* Specify node for execution */
    agent { 
        docker { image 'python:3.8.10' } 
    }

    stages {
        stage('checkout SCM') {
            steps {
                echo ">> Checkout from Github"
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: 'main']],
                    userRemoteConfigs: [[
                        url: 'git@github.com:lemsfaivre/test_api_jenkins',
                        credentialsId: '',
                    ]]
                ])
            }
        }
    
        stage('build') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('test') {
            steps {
                sh 'python test.py'
            }   
        }
    }
}