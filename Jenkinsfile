pipeline {
    agent any

    stages {
        stage('Build Java App') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo 'Build Completed so archiving the war file'
                    archiveArtifacts artifacts: '**/*.war', followSymlinks: false

                }
            }
        }
    }
}
