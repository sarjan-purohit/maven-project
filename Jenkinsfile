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
    }
}
