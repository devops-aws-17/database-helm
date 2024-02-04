pipeline {
    agent any

    stages {
        stage('connecting k8') {
            steps {
                sh 'kubectl config use-context arn:aws:eks:ap-south-2:844609451572:cluster/devops-eks-MzZhZjIe'
            }
        }
        stage('creating namesapace') {
            steps {
                sh '''
                myNamespace="database"
                kubectl get namespace | grep -q "^$myNamespace" || kubectl create namespace $myNamespace
                '''
            }
        }
      stage('helm install') {
            steps {
                sh 'helm upgrade --install database-helm $WORKSPACE --values $WORKSPACE/createat-mariadb.yaml --skip-crds --namespace database'
            }
        }
      stage('pods status') {
            steps {
                sh 'kubectl get pods -n database'
            }
      }
        
    }
}
