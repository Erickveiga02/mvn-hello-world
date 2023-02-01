pipeline {
   agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: k8s
    image: someimage:latest
    command:
    - sleep
    args:
    - infinity
    volumeMounts:
      - name: workspace-volume
        mountPath: /home/jenkins/agent
    workingDir: "/home/jenkins/agent"
      """
    }
 }
}
build()
unitTest()
