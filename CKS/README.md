# Install Kubernetes

### Prerequisites
VM1 - CKS-MASTER - Ubuntu 20.04 LTS / Disk 50Gb / 2 CPU / 8 Gb Men
VM2 - CKS-WORKER - Ubuntu 20.04 LTS / Disk 50Gb / 2 CPU / 8 Gb Men

___
#### CREATE cks-master VM using gcloud command
``` bash
gcloud compute instances create cks-master --zone=europe-west3-c \
--machine-type=e2-medium \
--image=ubuntu-2004-focal-v20220419 \
--image-project=ubuntu-os-cloud \
--boot-disk-size=50GB
```

#### CREATE cks-worker VM using gcloud command
``` bash
gcloud compute instances create cks-worker --zone=europe-west3-c \
--machine-type=e2-medium \
--image=ubuntu-2004-focal-v20220419 \
--image-project=ubuntu-os-cloud \
--boot-disk-size=50GB
```

##### you can use a region near you
https://cloud.google.com/compute/docs/regions-zones

___
#### INSTALL cks-master
``` bash
gcloud compute ssh cks-master
sudo -i
bash <(curl -s https://raw.githubusercontent.com/killer-sh/cks-course-environment/master/cluster-setup/latest/install_master.sh)
```

#### INSTALL cks-worker
``` bash
gcloud compute ssh cks-worker
sudo -i
bash <(curl -s https://raw.githubusercontent.com/killer-sh/cks-course-environment/master/cluster-setup/latest/install_worker.sh)
```
run the printed kubeadm-join-command from the master on the worker

___

#### Create Firewall Rules
``` bash
gcloud compute firewall-rules create nodeports --allow tcp:30000-40000
```