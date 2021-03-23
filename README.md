# Spark on Kubernetes with MinIO as object storage


Install minicube:
    
    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin/minikube
    
    minikube start
    minikube dashboard


Install kubectl:

    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

    kubectl version --client


Install helm:

    curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
    chmod 700 get_helm.sh
    ./get_helm.sh

    helm version


Install MinIO on Kubernetes:

    helm install minio --set accessKey=myaccesskey,secretKey=mysecretkey minio/minio

    kubectl get pods
    kubectl get svc
    kubectl get pvc


Install kubefwd:

    # download and install kubefwd from https://github.com/txn2/kubefwd/releases
    sudo -E kubefwd svc
