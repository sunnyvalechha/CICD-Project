Project Repo: https://github.com/jaiswaladi246/DevOps_Shack_Ultimate_Pipeline_12_march/blob/main/PHASE-1/2.%20K8-Setup.md

[On Master & Worker Node]

Create script for below commands and run together

    sudo apt-get update -y
    sudo apt install docker.io -y
    sudo chmod 666 /var/run/docker.sock
    sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
    sudo mkdir -p -m 755 /etc/apt/keyrings
    curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
    echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

    sudo apt update

    sudo apt install -y kubeadm=1.28.1-1.1 kubelet=1.28.1-1.1 kubectl=1.28.1-1.1

[On MasterNode]

    sudo kubeadm init --pod-network-cidr=10.244.0.0/16

Note: If above command does not work and show error, run **"kubeadm reset"** it will remove all k8 config then try again with above command.


[On WorkerNodes]    
    
    kubeadm join 172.31.3.178:6443 --token vmrxr6.50a17rd12e0h9ive \
        --discovery-token-ca-cert-hash sha256:49c13ef82a784fb63b06ba6908eab60ab0c5944482a5a0165a53f27b7549e572    

[On MasterNode]

    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config
    kubectl apply -f https://calico-v3-25.netlify.app/archive/v3.25/manifests/calico.yaml
    kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml



    

    
