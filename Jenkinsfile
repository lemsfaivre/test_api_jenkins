// Examples of groovy Jenkins files
// https://www.jenkins.io/doc/book/pipeline/docker/
// https://betterprogramming.pub/how-too-add-github-webhook-to-a-jenkins-pipeline-62b0be84e006

def runCommandInMyEnvironment(cmd) {
  sh "source venv/bin/activate; ${cmd}"
}

pipeline {
    /* Specify node for execution */
    agent any

    stages {
        stage('checkout SCM') {
            steps {
                echo ">> Checkout from Github"
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: 'main']],
                    userRemoteConfigs: [[
                        url: 'git@github.com:lemsfaivre/test_api_jenkins.git',
                        credentialsId: '',
                    ]]
                ])
            }
        }
        
        stage('Virtual environment') {
            steps {
                sh 'python3 -m venv venv'
            }
        }
    
        stage('build') {
            steps {
                runCommandInMyEnvironment('pip install -r requirements.txt')
            }
        }

        stage('install pytest') {
            steps {
                runCommandInMyEnvironment('python test.py')
            }   
        }
    }
}
