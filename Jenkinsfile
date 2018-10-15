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
                timeout(times:5,unit:days){
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
