pipeline {
    agent any

    stages {
        stage('connecting k8') {
            steps {
                sh 'kubectl config use-context arn:aws:eks:ap-south-2:844609451572:cluster/devops-eks-MzZhZjIe'
            }
        }
      stage('helm install') {
            steps {
                sh 'helm upgrade --install mariadb $WORKSPACE --values $WORKSPACE/created-mariadb.yaml --namespace database'
            }
        }
      stage('pods status') {
            steps {
                sh 'kubectl get pods -n database'
            }
      }
        
    }
}
