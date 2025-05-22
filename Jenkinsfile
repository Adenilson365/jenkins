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
                /var/jenkins_home/kubectl --kubeconfig=$KUBE_CONFIG get nodes
                ls -l /var/jenkins_home/
                ls -l /var/jenkins_home/k8s
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
 
                    sh ('/var/jenkins_home/kubectl apply --kubeconfig=$KUBE_CONFIG -f k8s/ --namespace=$NAMESPACE')

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
