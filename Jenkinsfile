pipeline { 
     agent {
    kubernetes {
      inheritFrom 'spring-petclinic-demo'
      defaultContainer 'jnlp'
      yaml '''
kind: Pod
metadata:
  name: ci
  namespace: ci-cd-tools
labels:
  component: mvn
spec:
  containers:
  - name: mvn
    image: maven:3-jdk-8-alpine
    command:
    - sleep
    args:
    - 9999999
    
'''
    }
  }

    stages { 

        stage('Build') { 
            steps { 
            container('mvn'){
               sh 'mvn package'
            }
            }
        }
        stage('Unit test'){
            steps{
                container('mvn'){
                    sh 'mvn test'
                }
            }
        }
         stage('Push Image'){
            steps{
                container('kaniko'){
                    sh  '/kaniko/executor --context `pwd` --destination erickveiga/hello-world-mvn'

                }
            }
         }
         stage('deploy'){
            steps{
                container('kubectl'){
                    sh  'kubectl apply -f k8s/deployment.yaml -n app --validate=false '
                    sh  'kubectl apply -f k8s/service.yaml -n app --validate=false '

                }
            }
         }
    }
}
