pipeline{
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn --version'
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "Now Archiving..."
                    archiveArtifacts artifacts: "**/*.war"
                }
            }
        }
        stage ('deploy to stage') {
            steps {
                build job: 'deploy to staging'
            }
        }
        stage ('deploy to prod'){
            steps{
                timeout(time:5,unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }
                build job:'deploy to prod'
            }
            post{
                success{
                    echo "success....."
                }
                failure{
                    echo "failure..."
                }
            }
        }
    }
}
