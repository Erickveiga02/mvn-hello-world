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

'''
    }
  }
 
    stages { 
         stage('kubectl'){
              steps{
               container('kubectl') { 
                sh 'kubectl get pods -n app'  
                    }
               }
          }     
          
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
    }
}
