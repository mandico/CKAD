Easily check the format of a yaml section within a K8S object : 
Kubectl explain pods --recursive | grep envFrom -A3 
Kubectl explain pods --recursive | less
