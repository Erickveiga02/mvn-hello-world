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
    image: erickveiga/maven-cli
'''
    }
  }
 
    stages { 
        stage('Build') { 
            steps { 
            containers('mvn'){
               sh 'mvn package'
            }
            }
        }
    }
}