# Spark on Kubernetes with MinIO as object storage

Spark-MinIO-K8s is a project for implementation of Spark on Kubernetes with MinIO as object storage, using docker, minicube, kubectl, helm, kubefwd and spark operator.


# Installation guide:

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

    helm repo add minio https://helm.min.io/
    helm install minio --set accessKey=myaccesskey,secretKey=mysecretkey minio/minio

    kubectl get pods
    kubectl get svc
    kubectl get pvc


Install kubefwd:

    # download and install kubefwd from https://github.com/txn2/kubefwd/releases
    wget https://github.com/txn2/kubefwd/releases/download/1.18.1/kubefwd_386.deb
    sudo dpkg -i kubefwd_386.deb

    sudo -E kubefwd svc


Download Spark:

    # download and install spark from https://spark.apache.org/downloads.html
    wget https://archive.apache.org/dist/spark/spark-3.1.1/spark-3.1.1-bin-hadoop3.2.tgz && \
    tar -xzvf spark-3.1.1-bin-hadoop3.2.tgz  -C /usr/local/ && \
    rm -rf spark-3.1.1-bin-hadoop3.2.tgz && \
    cd /usr/local/
    sudo ln -sT spark-3.1.1-bin-hadoop3.2 spark
    export SPARK_HOME=/usr/local/spark
    export PATH=$PATH:$SPARK_HOME/bin
    source ~/.zshrc # source ~/.bashrc

    spark-submit


Add MinIO jar file dependencies:

    wget https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk-bundle/1.11.375/aws-java-sdk-bundle-1.11.375.jar -P /usr/local/spark/jars/

    wget https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/3.2.0/hadoop-aws-3.2.0.jar \
    -P /usr/local/spark/jars/


Install Spark Operator:

    helm repo add spark-operator https://googlecloudplatform.github.io/spark-on-k8s-operator
    helm install sparkoperator spark-operator/spark-operator

    kubectl get pods