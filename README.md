# Install Seldon Core on EKS

 1. [Create your EKS cluster and authenticate kubectl](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html).
 1. Install [helm](https://docs.helm.sh/) on your cluster if it is not there already.
 ```
 kubectl -n kube-system create sa tiller
 kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller
 helm init --service-account tiller
 ```
 1. Install Seldon Custom Resource Definition. Set:
    * ```usage_metrics.enabled``` as appropriate.
    
```
helm install seldon-core-crd --name seldon-core-crd --repo https://storage.googleapis.com/seldon-charts \
     --set usage_metrics.enabled=true
```
 
 1. Install latest Seldon Core
 ```
   helm install seldon-core-aws --name seldon-core --repo https://storage.googleapis.com/seldon-aws-charts 
 ```

# Further Documentation

For further documentation on using Seldon Core visit the [Seldon Core project page](https://github.com/SeldonIO/seldon-core).

**Note at present you will need to use Ambassador as ingress for the APIs exposed**

# FAQs

## Install a particular version

Use the helm ```--version``` tag to install a particular version, e.g.:

 ```
   helm install seldon-core-aws --name seldon-core --repo https://storage.googleapis.com/seldon-aws-charts \
        --version 0.2.3
 ```

## Install in a particular namespace

Use the helm ```--namespace``` argument to install in a particular namespace


 ```
   helm install seldon-core-aws --name seldon-core --repo https://storage.googleapis.com/seldon-aws-charts \
        --namespace my-namespace
 ```
