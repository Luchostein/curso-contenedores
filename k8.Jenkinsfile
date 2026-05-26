pipeline {
    agent {
        kubernetes {
            yaml '''
apiVersion: v1
kind: Pod
spec:
    containers:
        - name: herramientas
          image: alpine-3.23
          command:
            -cat
          tty: true
'''
        }
    }
    stages {
        stage('Primer paso') {
            steps {
                sh 'echo "mensaje desde el terminal"'
            }
        }
        stage('Segundo paso') {
            agent {
                kubernetes {
                    defaultContainer: 'node'
                    yaml: '''
apiVersion: v1
kind: Pod
spec:
    containers:
        - name: node
          image: node:24
          command:
            - cat
        tty: true
'''
                }
            }
            steps {
                container('node') {
                    sh 'node --version'
                    sh 'npm --version'
                }
            }
        }
        stage('Tercer paso') {
            agent {
                kubernetes {
                    yaml: '''
apiVersion: v1
kind: Pod
spec:
    containers:
        - name: kubectl
          image: alpine/k8s:1.34.1
          command:
            - cat
          tty: trye
'''
                }
            }
            steps {
                container('kubectl') {
                    sh 'kubectl version --client'
                }
            }
        }
    }
}