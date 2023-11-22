# UPF-Evaluation
This Repository is about Evaluation of Different UPF Implementations, regarding SPGWU-UPF, P4-UPF and VPP-UPF



## 1. Prerequisites

### * Docker Installation: 

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

### * Docker Compose Installation:

Download Docker Compose from its official GitHub repository
```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.0.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
Apply executable permissions to the binary:
```
sudo chmod +x /usr/local/bin/docker-compose
```


## 2. Deployments
GENIKA LOGIS

### 2.1 SPGWU-UPF: 

The OpenAirInterface's 'oai-spgwu-tiny' is an enhanced version of the Serving and Packet Data Network Gateway User plane (SPGW-U), a key component in 4G/LTE networks for routing and forwarding user data. Initially designed for 4G/LTE based on 3GPP standards, it has been updated to also support 5G networks.
The complete 5G architecture (based on SPGWU-UPF) can be depicted in the figure below:

![Alt text](/figures/spgwu_arch.png)

In order to Deploy this setup you have to execute the following commands on your host machine:

* Deploy the 5G Core Network based on SPGWU:
```
sudo bash deploy-spgwu-based-core.sh
```
* Deploy 5G RAN based on UERANSIM:
```
sudo bash deploy-ueransim-spgwu.sh
```

When both commands are executed, your SPGWU-based deployment should be working properly. 

- You may ckeck the status of your containers with:
```
sudo docker ps -a
```
- You may ckeck the logs of each network function by executing the following command (generates .txt log files):
```
bash generate-logs.sh
```
- You can destroy the whole architecture by executing the following commands:
```
bash destroy-spgwu-based-core.sh
```
```
bash destroy-spgwu-ueransim.sh
```

### 2.2 VPP-UPF: 

The OpenAirInterface's 'oai-spgwu-tiny' is an enhanced version of the Serving and Packet Data Network Gateway User plane (SPGW-U), a key component in 4G/LTE networks for routing and forwarding user data. Initially designed for 4G/LTE based on 3GPP standards, it has been updated to also support 5G networks.
The complete 5G architecture (based on SPGWU-UPF) can be depicted in the figure below:

![Alt text](/figures/vpp_arch.png)

In order to Deploy this setup you have to execute the following commands on your host machine:

* Deploy the 5G Core Network based on VPP:
```
sudo bash deploy-vpp-based-core.sh
```
* Deploy 5G RAN based on UERANSIM:
```
sudo bash deploy-ueransim-vpp.sh
```

When both commands are executed, your SPGWU-based deployment should be working properly. 

- You may ckeck the status of your containers with:
```
sudo docker ps -a
```
- You may ckeck the logs of each network function by executing the following command (generates .txt log files):
```
bash generate-logs.sh
```
- You can destroy the whole architecture by executing the following commands:
```
bash destroy-vpp-based-core.sh
```
```
bash destroy-vpp-ueransim.sh
```

