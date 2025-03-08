pipeline {
    agent any

    stages{
        stage('Build Java App') {
            steps {
                sh 'mvn -f pom.xml cleam -package'
            }
             post {
                 success {
                     echo 'Build Completed so archiving the war file'
                    archiveArtifacts artifacts: '**/*.war', followSymlinks: false
//                 }
//             }
//         }
//         stage('UNIT TEST') {
//             steps {
//                 sh 'mvn -f pom.xml test'
//             }
//         }
//         stage('Checkstyle Analysis') {
//             steps {
//                 sh 'mvn -f pom.xml checkstyle:checkstyle'
//             }
//         }
//         stage('Sonar Analysis') {
//             steps {
//                 withSonarQubeEnv('sonar') {
//                     sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=java-tomcat-sample \
//                         -Dsonar.projectName=java-tomcat-sample \
//                         -Dsonar.projectVersion=4.0 \
//                         -Dsonar.sources=src/ \
//                         -Dsonar.junit.reportsPath=target/surefire-reports/ \
//                         -Dsonar.jacoco.reportsPath=target/jacoco.exec \
//                         -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
//                 }
//             }
//         }
// stage("UploadArtifact") {
//             steps {
//                 nexusArtifactUploader(
//                     nexusVersion: 'nexus3',
//                     protocol: 'http',
//                     nexusUrl: '172.31.25.191:8081',
//                     groupId: 'QA',
//                     version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
//                     repository: 'java-app',
//                     credentialsId: 'sonartypecred',
//                     artifacts: [
//                         [artifactId: 'java-tomcat-sample',
//                          classifier: '',
//                          file: 'target/java-tomcat-maven-example.war',
//                          type: 'war']
//                     ]
//                 )
//             }
        }
    }
}