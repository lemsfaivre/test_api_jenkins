pipeline {
    /* Specify node for execution */
    agent any
    /*agent { 
        docker { image 'python:3.7.2' } 
    }*/

    stages {
        stage('checkout SCM') {
            steps {
                echo ">> Checkout from Github"
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