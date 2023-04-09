podTemplate(yaml: '''
kind: Pod
metadata:
  name: kubectl
  namespace: ibrahim
spec:
  containers:
  - name: kubectl
    image: portainer/kubectl-shell
    imagePullPolicy: IfNotPresent
    command: ["tail", "-f", "/dev/null"]
    tty: true
''') {
    node (POD_LABEL) {
        stage('Apply Kubernetes files') {
            checkout scm
            container('kubectl') {
                withKubeConfig([namespace: "ibrahim"]) {
                    sh 'kubectl apply -f deployment.yaml -n ibrahim'
                }
            }
        }
    }
}
