pipeline{
    agent any
    stages{
        stage('Build'){
            setps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Now Archiving..."
                    archivArtifacts artifacts: "**/*.war"
                }
            }
        }
    }
}
