pipeline{
    agent { node {label 'agent-1'} }
    stages{
        stage('Build')
        {
            steps
            {
                echo "Building..."
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
                error "Hello error"
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