// Examples of groovy Jenkins files
// https://www.jenkins.io/doc/book/pipeline/docker/
// https://betterprogramming.pub/how-too-add-github-webhook-to-a-jenkins-pipeline-62b0be84e006
// https://gist.github.com/jubel-han/0e669dbbfa9e966f0b79a91730edc806

def runCommandInMyEnvironment(cmd) {
  sh ". venv/bin/activate; ${cmd}"
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
                runCommandInMyEnvironment('pip install pytest')
                runCommandInMyEnvironment('pip install pytest-cov')
            }   
        }
      
        stage('run tests') {
            steps {
                runCommandInMyEnvironment('pytest tests --junitxml=reports/result.xml --cov=api --cov-report=xml:reports/coverage.xml')
                step([$class: 'CoberturaPublisher', 
                        coberturaReportFile: "reports/coverage.xml"
                      ])
                junit "reports/result.xml"
            }   
        }
    }
}
