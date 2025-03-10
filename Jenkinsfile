pipeline {
    agent {
        label 'slave-node1' 
    }
    environment {
        dockerImages = "suvam1/jenkins-project"
    }
    stages {
        stage('Build Java App') {
            agent {
                label 'slave-node1'
            }
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
            agent {
                label 'slave-node1'
            }   
            steps {
                copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: env.JOB_NAME, selector: specific(env.BUILD_NUMBER)
                echo "creating docker image "
                sh 'whoami'
                sh "docker build -t $dockerImages:$BUILD_NUMBER ."
            }
        }
        stage('Trivy Scan for Docker Image'){
            steps {
                sh 'echo'
                sh 'trivy image --exit-code 1 --severity HIGH,CRITICAL --ignore-unfixed $dockerImages:$BUILD_NUMBER'
            }
        }

        stage('Push Image') {
            agent {
                label 'slave-node1'
            }
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
