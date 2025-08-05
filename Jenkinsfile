pipeline {
    agent any
    environment {
        KUBECONFIG_CRED = 'kubeconfig-id' // Replace with Jenkins credential ID
        REGISTRY = "registry.shuttlewhizz.com:5000"
        IMAGE = "${REGISTRY}/node-js-app"
        K8S_DEPLOYMENT_NAME = "nodejs-app"
        K8S_NAMESPACE = "node-js"
        REGISTRY_CRED = 'registry-creds' // <- your credentials ID
    }
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/guravsuyash/nodejsapp.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t $IMAGE:latest .'
            }
        }
        stage('Push') {
            // steps {
            //     sh 'docker push $IMAGE:latest'
            // }
            steps {
                withCredentials([usernamePassword(credentialsId: "${REGISTRY_CRED}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo $DOCKER_PASS | docker login $REGISTRY -u $DOCKER_USER --password-stdin
                        docker push $IMAGE:latest
                    '''
                }
            }
        }
        // stage('Deploy') {
        //     steps {
        //         sh "kubectl create namespace $K8S_NAMESPACE"
        //         // sh "kubectl apply -f k8s/deployment.yaml"
        //         sh "kubectl apply -f k8s"
        //         // sh "kubectl apply -f k8s/service.yaml"
        //     }
        // }
        stage('Deploy') {
            steps {
                withCredentials([file(credentialsId: "${KUBECONFIG_CRED}", variable: 'KUBECONFIG')]) {
                    sh 'kubectl config get-contexts'  // test access
                    // sh "kubectl create namespace $K8S_NAMESPACE --dry-run=client -o yaml | kubectl apply -f -"
                    // sh "kubectl apply -f k8s -n $K8S_NAMESPACE"
                }
            }
        }

    }
    post {
        failure {
            // sh 'kubectl rollout undo deployment/your-deployment'
            sh "kubectl rollout undo deployment/$K8S_DEPLOYMENT_NAME -n $K8S_NAMESPACE || echo 'No rollback available'"
        }
    }
}
