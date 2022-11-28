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
    image: csanchez/kaniko
    command:
    - sleep
    args:
    - 9999999
    volumeMounts:
     - name: kaniko-secret
       mountPath: /kaniko/.docker
  volumes:
    - name: kaniko-secret
      secret:
         secretName: docker-credentials
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
                    sh '/kaniko/executor --dockerfile Dockerfile --destination=erickveiga/app:${env.BUILD_ID}'
                }
            }
         }
    }
}
