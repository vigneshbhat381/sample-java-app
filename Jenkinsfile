pipeline {
    agent any
    environment {
        APP_HOME='/home/app'
        PRAGRA_BATCH='devs'
    }
    options { 
        quietPeriod(30) 
    }
    parameters { 
            choice(name: 'ENV_TO_DEPLOY', 
            choices: ['ST', 'UAT', 'STAGING'], description: 'Select a Env to deploy') 

             booleanParam(name: 'RUN', defaultValue: true, description: 'SELECT TO RUN')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools{
        maven  'Maven3'
        jdk 'jdk8'
    }

    stages {
        stage('Git CheckoutOut'){
            environment{
                GIT_REPO='https://github.com/atinsingh/sample-java-app.git'
            }
            steps {
                git "${GIT_REPO}"
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

         stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }

         stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        always {
            echo 'ALL GOOD '
            echo "${BRANCH_NAME}  : ${JOB_NAME}"
        }
    }


}


// && 
