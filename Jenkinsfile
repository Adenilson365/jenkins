pipeline {
    agent any

    environment {
        KUBE_CONFIG = credentials('kubeconfig') // ID da credencial com o kubeconfig
        NAMESPACE = "web" // Altere se os manifests tiverem outro namespace
    }



    stages {

        stage('kubectl') {
            steps {
            sh '''
                /var/jenkins_home/kubectl version 
            '''
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'dev', url: 'https://github.com/Adenilson365/jenkins'
            }
        }

        stage('Apply Kubernetes Manifests') {
            steps {
 
                    sh ('kubectl apply --kubeconfig=$KUBE_CONFIG -f k8s/ --namespace=$NAMESPACE')

            }
        }
    }

    post {
        success {
            echo "✅ Manifestos aplicados com sucesso no Kubernetes!"
        }
        failure {
            echo "❌ Falha ao aplicar os manifestos."
        }
    }
}
