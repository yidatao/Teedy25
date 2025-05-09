// Lab 13
pipeline {
    agent any

    environment {
        DEPLOYMENT_NAME = "teedy25-demo"
        CONTAINER_NAME = "teedy-original-4xmtc"
        IMAGE_NAME = "yidatao/teedy_original:v3.0"
    }

    stages {
        stage('Start Minikube') {
            steps {
                sh '''
                    if ! minikube status | grep -q "Running"; then
                        echo "Starting Minikube..."
                        minikube start
                    else
                        echo "Minikube already running."
                    fi
                '''
            }
        }

        stage('Set Image') {
            steps {
                sh '''
                    echo "Setting image for deployment..."
                    kubectl set image deployment/${DEPLOYMENT_NAME} ${CONTAINER_NAME}=${IMAGE_NAME}
                '''
            }
        }

        stage('Verify') {
            steps {
                sh 'kubectl rollout status deployment/${DEPLOYMENT_NAME}'
                sh 'kubectl get pods'
            }
        }
    }
}



// Lab 12
// pipeline {
//     environment {
//         registry = "yidatao/teedy_original"
//         registryCredential = 'dockerpush'
//         dockerImage = ''
//     }
//     agent any
//     stages {
//         stage('Maven build') { 
//             steps {
//                 sh 'mvn -B -DskipTests clean package' 
//             }
//         }
        
//         stage('Build docker image') { 
//             steps {
//                script {
//                     dockerImage = docker.build registry + ":v3.0"
//                 }
//             }
//         }

//         stage("Publish to dockerhub") {
//             steps {
//                 script {
//                     docker.withRegistry( '', registryCredential ) {
//                     dockerImage.push()
//                     } 
//                 }                    
//             }
//         }

//         stage("Run containers"){
//             steps{
//                 script{
//                     dockerImage.run("-d -p 8888:8080 --rm --name newContainer")
//                 }
//             }
//         }
        
//     }
// }

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
