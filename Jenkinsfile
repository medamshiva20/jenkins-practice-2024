pipeline{
    agent { node {label 'agent-1'} }
     options {
        timeout(time: 1, unit: 'HOURS') 
    }
    //  triggers {
    //     cron('* * * * *')
    // }
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
        stage('Input') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo "Hello, ${PERSON}, nice to meet you."
            }
        }
        stage('PROD Deploy') {
            when {
                environment name: 'USER', value: 'sivamedam'
            }
            steps {
                echo 'Deploying to PROD'
            }
        }
        stage('Parallel stage'){
            parallel{
                stage('Branch A')
                {
                    steps{
                        echo "On branch A"
                        sh '''
                        sleep 10
                        '''
                    }
                }
                stage('Branch B')
                {
                    steps{
                        echo "On branch B"
                        sh '''
                        sleep 10
                        '''
                    }
                }
               stage('Branch C')
               {
                stages{
                    stage('Nested 1'){
                        steps{
                            echo "In stage Nested 1 within Branch C"
                            sh '''
                            sleep 10
                            '''
                        }
                    }
                    stage('Nested 2'){
                        steps{
                            echo "In stage Nested 2 within Branch C"
                            sh '''
                            sleep 10
                            '''
                        }
                    }
                }
               }
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