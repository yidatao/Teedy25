// Lab 12
pipeline {
    environment {
        registry = "yidatao/teedy_original"
        registryCredential = 'dockerpush'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Maven build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        
        stage('Build docker image') { 
            steps {
               script {
                    dockerImage = docker.build registry + ":v3.0"
                }
            }
        }

        stage("Publish to dockerhub") {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                    } 
                }                    
            }
        }

        stage("Run containers"){
            steps{
                script{
                    dockerImage.run("-d -p 8888:8080 --rm --name newContainer")
                }
            }
        }
        
    }
}

// Lab 11
// pipeline {
//     agent any

//     stages {
//         stage('Clean') {
//             steps {
//                 sh 'mvn clean'
//             }
//         }

//         stage('Compile') {
//             steps {
//                 sh 'mvn compile'
//             }
//         }

//         stage('Test') {
//             steps {
//                 sh 'mvn test -Dmaven.test.failure.ignore=true'
//             }
//         }

//         stage('PMD') {
//             steps {
//                 sh 'mvn pmd:pmd'
//             }
//         }

//         stage('JaCoCo') {
//             steps {
//                 sh 'mvn jacoco:report'
//             }
//         }

//         stage('Javadoc') {
//             steps {
//                 sh 'mvn javadoc:javadoc'
//             }
//         }

//         stage('Site') {
//             steps {
//                 sh 'mvn site'
//             }
//         }

//         stage('Package') {
//             steps {
//                 sh 'mvn package -DskipTests'
//             }
//         }
//     }

//     post {
//         always {
//             archiveArtifacts artifacts: '**/target/site/**/*.*', fingerprint: true
//             archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
//             archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
//             junit '**/target/surefire-reports/*.xml'
//         }
//     }

// }
