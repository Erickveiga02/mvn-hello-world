def podTemplate = """
apiVersion: v1
kind: Pod
name: teste
namespace: ci-cd-tools
spec:
  containers:
  - name: k8s
    image: someimage:latest
    command:
    - sleep
    args:
    - infinity
"""
pipeline {
  agent {
    kubernetes {
          yaml podTemplate
          defaultContainer 'k8s'
    }
build()
unitTest()
}