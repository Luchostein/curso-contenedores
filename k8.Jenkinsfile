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
                    sh 'kubectl version --client'
                    sh 'node --version'
                    sh 'npm --version'
                }
            }
        }
    }
}