# How to Create a Custom Cluster of Three nodes(physical or virtual) using Rancher


Note: You will get $200 credit when register on Google Cloud Console so that you can use free crdit in creating instances.

# Step 1: 
 Create 4 Google Compute Instance(with Ubuntu 16.04 image) from Google Cloud Console with (http and https) trafic rules applied .One instance is for Deploying Rancher Server and with other 3 instances we will create a Cluster with the help of Rancher UI.

# Step 2: 
Install Docker for Ubuntu 16.04 on all 4 nodes  from https://docs.docker.com/install/linux/docker-ce/ubuntu/  step by step.

* sudo apt-get update
* sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common 
* curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
* sudo apt-key fingerprint 0EBFCD88
* sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
* sudo apt-get update
* sudo apt-get install docker-ce docker-ce-cli containerd.io

# Step 3: 
* Log in to your Linux instance using your preferred from Google cloud console dashboard
* From your shell, enter the following command:$ sudo docker run -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher
* Rancher Installed successfully.

# Step 4: 
Log in to Rancher to begin using the application. After you log in, you’ll make some one-time configurations.
* Open a web browser and enter the IP address of your host: https://<SERVER_IP>.Replace <SERVER_IP> with your host IP address.
* When prompted, create a password for the default admin account there cowpoke!
* Set the Rancher Server URL. The URL can either be an IP address or a host name. However, each node added to your cluster must be able to connect to this URL.If you use a hostname in the URL, this hostname must be resolvable by DNS on the nodes you want to add to you cluster.
Step 4: 
Create a Cluster
Welcome to Rancher! You are now able to create your first Kubernetes cluster.
In this task, you can use the versatile Custom option. This option lets you add any Linux host (cloud-hosted VM, on-premise VM, or bare-metal) to be used in a cluster.
* From the Clusters page, click Add Cluster.
* Choose Custom.
* Enter a Cluster Name.
* Skip Member Roles and Cluster Options. We’ll tell you about them later.
* Click Next.
* From the three remain nodes create 1 node as Master node and Other nodes as Worker Node.
* From Node Role, select the roles: etcd, Control ,  copy the below command and run it on all master node e.g: 
```sudo docker run -d --privileged --restart=unless-stopped --net=host -v /etc/kubernetes:/etc/kubernetes -v /var/run:/var/run rancher/rancher-agent:v2.2.6 --server https://<Your_IP>:<Port> --token brhwsv2gsk8c69ctsnvfstzh6qnjdqfltmxn67q7lbkkmf5fgz76wm --ca-checksum 015108c6002265c45e7b4e85fb2371cfaef5987fb26fbc016ff88b1f7e1a77d0 --etcd --controlplane```
* From Node Role, select the roles: Worker copy the below command and run it on all workers node  e:g.
```sudo docker run -d --privileged --restart=unless-stopped --net=host -v /etc/kubernetes:/etc/kubernetes -v /var/run:/var/run rancher/rancher-agent:v2.2.6 --server https://<Your_IP>:<Port> --token brhwsv2gsk8c69ctsnvfstzh6qnjdqfltmxn67q7lbkkmf5fgz76wm --ca-checksum 015108c6002265c45e7b4e85fb2371cfaef5987fb26fbc016ff88b1f7e1a77d0 —worker```
* Optional: Rancher auto-detects the IP addresses used for Rancher communication and cluster communication. You can override these using Public Address and Internal Address in the Node Address section.
* Skip the Labels stuff. It’s not important for now.
* Copy the command displayed on screen to your clipboard.
* Log in to your Linux host using your preferred shell, such as PuTTy or a remote Terminal connection. Run the command copied to your clipboard.
* When you finish running the command on your Linux host, click Done

