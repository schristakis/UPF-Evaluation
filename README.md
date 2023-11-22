# UPF-Evaluation
This Repository is about Evaluation of Different UPF Implementations, regarding SPGWU-UPF, P4-UPF and VPP-UPF

specs klp

## 1. Prerequisites

### 1.1 Docker Installation: 

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

### 1.2 Docker Compose Installation:

Download Docker Compose from its official GitHub repository
```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.0.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
Apply executable permissions to the binary:
```
sudo chmod +x /usr/local/bin/docker-compose
```


## 2. Deployments
Each UPF deployment has one folder for the core network configuration (i.e. spgwu, vpp, p4) and one folder for the respective UERANSIM deployment (i.e. UERASNIM-spgwu, UERASNIM-vpp, UERASNIM-p4). You can manually deploy everything by using the docker-compose -f command. However in this tutorial we have generated scipts for deploying and destroying each deployment very easily. 

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
bash generate-logs-spgwu.sh
```
- You can destroy the whole architecture by executing the following commands:
```
bash destroy-spgwu-based-core.sh
```
```
bash destroy-spgwu-ueransim.sh
```

### 2.2 VPP-UPF: 

Vector Packet Processing (VPP) is a high-speed, high-efficiency packet processing framework that enhances data plane performance in networks. Unlike traditional methods, VPP uses vector processing to handle multiple packets simultaneously, leveraging modern CPUs' SIMD capabilities for parallel processing. This results in high throughput and low latency, often outperforming specialized hardware. VPP incorporates the Data Plane Development Kit (DPDK) for direct NIC access, bypassing the OS network stack, and distributes workloads across multiple CPU cores for scalability. VPP is particularly beneficial in 5G networks, where it's used for User Plane Function solutions, handling high-speed data with low response times.

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

When both commands are executed, your VPP-based deployment should be working properly. 

- You may ckeck the status of your containers with:
```
sudo docker ps -a
```
- You may ckeck the logs of each network function by executing the following command (generates .txt log files):
```
bash generate-logs-vpp.sh
```
- You can destroy the whole architecture by executing the following commands:
```
bash destroy-vpp-based-core.sh
```
```
bash destroy-vpp-ueransim.sh
```



### 2.3 P4-SWITCH-UPF: 

P4, a programming language, revolutionizes packet switches for 5G networks by turning static hardware into programmable devices, melding hardware speed with software flexibility. Our setup includes ONOS (managing P4-switch User Plane Function), Stratum (guiding physical switches), and the PFCP Agent for control plane links. ONOS controls network programming and policy updates, while Stratum implements ONOS's commands in hardware. The PFCP Agent facilitates communication between the control plane and P4-switches. Displayed in the Figures, our architecture integrates ONOS and OpenAirInterface on a server, with UPF and Stratum running in the P4 switch. This system is unified via a management switch and a user-plane network linked by a QFSP cable to the P4 switch.


<p align="center">
  <img src="/figures/p4_distribution.png" width="400" /> 
  <img src="/figures/p4_arch.png" width="400" />
</p>


#### Configuration

For the P4-Switch deployment we utilized the Wedge100BF-32X Switch. The procedure to make it work properly is described below:

i)	Connect the switch to the power and wait for the Baseboard Management Controller (BMC) to finish booting.

ii)	Connect the switch with a physical server via a rollover cable on the console ethernet port of the switch.

iii)	Connect the switch with a physical server via ethernet cable on the management ethernet port of the switch

iv)	Connect to the switch via the serial console (using screen):
```
screen /dev/ttyS1 9600
```
Replace "/dev/ttyS1" with the appropriate serial port if needed.

v)	Log into the BMC with the login: 

username: root 

password: 0penBmc

vi)	Connect to the ONIE environment by running sol.sh
```
sol.sh
```

vii)	Stop the dhcp discovery by running:
```
onie-discovery-stop
```

viii)	Add a static IP to eth0, matching the subnet of the server you are connected through the management port.

ix)	Build ONL installer by using a pre-built ONL installer

x)	Obtain the ONL installer to the switch from a TFTP or HTTP Server or transfer the installer via SCP command.

xi)	Install the ONL installer by: onie-nos-install onl-installer-file using the console connection

xii)	After the switch is booted with the ONL, login with: 

username: root 

password: onl

xiii)	Bring the ma1  interface up (using a different IP from bmc’s eth0)  and connect with ssh using the management connection

xiv)	Add a gateway and DNS server and make the IP configurations persistent via /etc/network/interfaces 



Finally, in order to Deploy this setup, you have to execute the following commands on your host machine:

* Deploy the 5G Core Network based on P4-Switch:
```
sudo bash deploy-p4-based-core.sh
```
* Deploy 5G RAN based on UERANSIM:
```
sudo bash deploy-ueransim-p4.sh
```

When both commands are executed, your P4-Switch-based deployment should be working properly. 

- You may ckeck the status of your containers with:
```
sudo docker ps -a
```
- You may ckeck the logs of each network function by executing the following command (generates .txt log files):
```
bash generate-logs-p4.sh
```
- You can destroy the whole architecture by executing the following commands:
```
bash destroy-p4-based-core.sh
```
```
bash destroy-p4-ueransim.sh
```

