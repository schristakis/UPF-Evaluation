# UPF-Evaluation
This Repository is about Evaluation of Different UPF Implementations, regarding SPGWU-UPF, P4-UPF and VPP-UPF


## 1. Prerequisites

* Docker Installation: 

Update:
```
sudo apt-get update
```
Install Docker:
```
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
Enable & start Docker with the following commands:
```
sudo systemctl enable docker
```

```
sudo systemctl start docker
```

* Docker Compose Installation:

Download Docker Compose from its official GitHub repository
```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.0.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
Apply executable permissions to the binary:
```
sudo systemctl start docker
```
