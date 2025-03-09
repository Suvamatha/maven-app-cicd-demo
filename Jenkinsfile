pipeline {
    agent any
    environment {
        dockerImages = "suvam1/jenkins-project"
    }
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
        stage('Create Docker image') {
            steps {
                copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: env.JOB_NAME, selector: specific(env.BUILD_NUMBER)
                echo "creating docker image "
                sh "docker build -t $dockerImages:$BUILD_NUMBER ."
            }
        }

        stage('Push Image') {
            steps {
                withDockerRegistry(credentialsId: 'dockerhub-credentials', url: ''){
                    sh '''
                    docker push $dockerImages:$BUILD_NUMBER
                    '''
                }
            }
        }
    }
}
