# devop

## Vagrant Kubernetes
[![ko-fi](https://www.ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/W7W3ZIV7)

```shell
git clone https://github.com/ruifigueiredo/devop.git
cd devop
vagrant up
```

### Log in to the master node to verify the cluster configurations.

```shell
vagrant status
vagrant ssh master
```

```shell
kubectl top nodes
```

### List all the pods in kube-system namespace and ensure it is in running state.

```shell
kubectl get po -n kube-system
```

### Deploy a sample Nginx app and see if you can access it over the nodePort.

```shell
kubectl apply -f https://raw.githubusercontent.com/scriptcamp/kubeadm-scripts/main/manifests/sample-app.yaml
```
You should be able to access Nginx on any of the node’s IPs on port 32000. For example, http://10.0.0.11:32000

### To shutdown the cluster,

```shell
vagrant halt
```

### To restart the cluster,

```shell
vagrant up
```

### To destroy the cluster,

```shell
vagrant destroy -f
```


### Access Kubernetes Cluster From Workstation Terminal

Once Vagrant execution is successful, you will see a configs folder with a few files (config, join.sh, and token) inside the cloned repo. These are generated during the run time.

Copy the config file to your $HOME/.kube folder if you want to interact with the cluster from your workstation terminal. You should have kubectl installed on your workstation.

For example, I did the following in my mac keeping vagrant-kubeadm-kubernetes folder as the current directory.

```shell
mkdir -p $HOME/.kube
cp configs/config $HOME/.kube
```

Alternatively, you can set a Kubeconfig env variable as shown below. Make sure you execute the command from the configs folder where you have the config file.

```shell
export KUBECONFIG=$(PWD)/config
```

Once you copy the kubeconfig (config) file to your local $HOME/.kube directory you can run the kubectl command against the cluster and access the kubernetes dashboard.

Run kubectl proxy to access the Kubernetes dashboard.

```shell
kubectl proxy
```

The token file inside the configs folder contains the sign-in token for the kubernetes dashboard. If you want to use the kubernetes dashboard, use the token and log in from the following URL

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login
