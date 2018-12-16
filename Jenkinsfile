pipeline {
    agent{
        label 'node1'
    }
      triggers {
            cron('* * * * *')
    }
    stages {
       
        //Stage to do checkout from scm
        stage('Checkout'){
            steps{
                    git( branch : 'master', url: 'https://github.com/atinsingh/sample-java-app.git')    
                    sh 'echo hello world'
                }
                
        }
        
        //Stage to run maven clean

        stage('Clean') {
            steps {
                    sh 'chmod +x mvnw'
                    sh './mvnw clean'
                }
            
           
            post {
                failure {
                    mail bcc: '', body: 'Some thing gone wrong in cleaning', cc: '', from: '', replyTo: '', subject: 'Check build', to: 'atin@pragra.co'
                }
            }
        }

        stage('Compile') {
            steps {
              
                 sh './mvnw compile'
                
            }
           
        }
        
    }
  
}