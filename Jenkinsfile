pipeline{
    agent { node {label 'agent-1'} }
     options {
        timeout(time: 1, unit: 'HOURS') 
    }
     environment { 
        USER = "sivamedam"
    }
    stages{
        stage('Build')
        {
            steps
            {
                echo "Building..."
                sh '''
                  ls -ltr
                  pwd
                  cd ../
                  printenv
                '''
            }
        }
        stage('Test')
        {
            steps{
                echo "Testing..."
            }
        }
        stage('Deploy')
        {
            steps{
                echo "Deploying..."
               // error "Hello error"
            }
        }
        stage('Example')
        {
        environment{
        AUTH = credentials('ssh-auth')
        }
        steps{
            sh '''
              printenv
            '''
        }
        }
    }
    post{
        always{
            echo "This will run whether job is success or failure"
        }
        success{
            echo "This will run when job is success"
        }
        failure{
            echo "This will run when failure"
        }
    }
}