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
'''
    }
  }
 
    stages { 
        stage('Build') { 
        containers('mvn')
            steps { 
               sh 'mvn clean install'
            }
        }
    }
}