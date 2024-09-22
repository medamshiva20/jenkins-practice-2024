pipeline{
    agent { node {label 'agent-1'} }
     options {
        timeout(time: 1, unit: 'HOURS') 
    }
     triggers {
        cron('* * * * *')
    }
     environment { 
        USER = "sivamedam"
    }
        parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
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
        stage('params') {
            steps {
                echo "Hello ${params.PERSON}"

                echo "Biography: ${params.BIOGRAPHY}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Password: ${params.PASSWORD}"
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