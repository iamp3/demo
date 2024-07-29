Deploying Airflow on Kubernetes
-------------------------------

### Overview

This repository provides instructions and Kubernetes manifests for deploying Apache Airflow on a Kubernetes cluster. It assumes basic familiarity with Kubernetes and Airflow.

### Prerequisites

*   A Kubernetes cluster with necessary RBAC permissions.
    
*   kubectl command-line tool configured to interact with your cluster.
    
*   helm package manager installed (optional, for Helm-based deployment).
    
*   Docker or a compatible container runtime.
    

### Deployment Options

This repository offers helm-chart deployment method:

1.  helm repo add apache-airflow https://airflow.apache.org
2.  helm repo update
3. **Customize values.yaml:**Use Helm's values.yaml file to customize the Airflow deployment. Refer to the values.yaml file to see all options. 
4. helm upgrade --install airflow apache-airflow/airflow --create-namespace -n airflow -f values.yaml 
5. kubectl get pods,svc -n airflow  
    

### Accessing Airflow

Once the deployment is complete, you can access the Airflow UI by:

*   Exposing the Airflow service as a NodePort or LoadBalancer.
*   Using kubectl port-forward to access a specific pod: kubectl port-forward svc/airflow-webserver 8080:8080 -n airflow
    
    
### Deploying new DAGs:

I used this option for deploying new DAGs: https://airflow.apache.org/docs/helm-chart/stable/manage-dags-files.html#mounting-dags-using-git-sync-sidecar-without-persistence
To me, it's more of a gitops approach to focus on development and just push the code of new DAGs into the git repository, then it will be automatically updated on the airflow side. 
