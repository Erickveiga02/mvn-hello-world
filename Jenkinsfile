pipeline { 
     agent {
    kubernetes {
      label 'spring-petclinic-demo'
      defaultContainer 'jnlp'
      yaml '''
kind: Pod
metadata:
  name: ci
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
  - name: kubectl
    image: amaceog/kubectl
    command:
    - sleep
    args:
    - 9999999
  - name: kaniko
    image: gcr.io/kaniko-project/executor:debug
    command:
    - sleep
    args:
    - 9999999
    volumeMounts:
    - name: kaniko-secret
      mountPath: /kaniko/.docker
  restartPolicy: Never
  volumes:
  - name: kaniko-secret
    secret:
       secretName: regcred
       items:
       - key: .dockerconfigjson
         path: config.json
    
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