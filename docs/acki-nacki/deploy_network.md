## **Generating BLS-keys**

### **Prerequisites:**

* cargo
* [tvm-cli](https://github.com/tvmlabs/tvm-cli/releases)
* python3

### **Install bls_keypair_gen**

```bash
cd helpers/bls_keypair_gen
cargo install --path .
```

### **Set the number of validators**

```bash
cd ../blockchain_config
```

Edit Python script (generate_keys_and_bc_config.py) to set the number of validators and output paths for BLS-keychain file and blockchain config file:

```python
NUMBER_OF_VALIDATORS = 12
OUTPUT_CONFIG = 'blockchain.conf.json'
BLS_PUBLICS_PATH = 'bls_publics_12.keys.json'
```

### **Run the python script**

```bash
python3 generate_keys_and_bc_config.py
```

The set of the key pairs for the validators will be created in the current folder.



## **Deploying Acki Nacki (with Ansible)**



### **Prerequisites:**


* [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

Put the `acki-nacki-vendored-main.zip` archive into the `files` folder for everything to work correctly without errors.


### **Build the hosts inventory**


Create (Build) the `inventory.yml` file.

Specify all your hosts that will run Acki Nacki nodes, paying special attention to Block Producer (BP) (collator) node.


!!! Example "For example"

    This way you can build the inventory file with some important moments commented:

    ```yaml
    all:
    hosts:
        node[1:5].mydomain.com: # this pattern should ideally match all the nodes to be deployed
        # replace with your SSH port and username, that should have sudo (passwordless or use -K)
        ansible_port: 22
        ansible_user: ubuntu
        # Archive name must match the name of the code zip archive downloaded from github and put in files folder
        # DO NOT rename archive after downloading from github!
        ARCHIVE_NAME: acki-nacki-vendored-main
        # Root directory path, in general, should not be modified
        ROOT_DIR: /opt/ackinacki
        # if you have a large fast volume on the server, it may be preferable to point this folder to it
        MNT_DATA: /var/data
        # must point to the domain of the BP collator (first node)
        STATIC_STORAGES: "http://node1.mydomain.com/storage/node-1/"
        # must be a list of IP:10000 of every node in deployment
        GOSSIP_SEEDS: 1.1.1.1:10000,2.2.2.2:10000,3.3.3.3:10000,4.4.4.4:10000,5.5.5.5:10000
        BIND_PORT: 8500
        BIND_API_PORT: 8600
        BIND_GOSSIP_PORT: 10000

    collators:
    hosts:
        # must match the BP (collator) (first) node
        node1.mydomain.com:
        ACKINACKI_ARANGODB_PUBLIC_PORT: 8529
        # must point to the IP of the BP (collator) (first node)
        ARANGODB_ENDPOINT: 1.1.1.1:8529
        # must point to the domain of the BP (collator) (first node)
        ARANGODB_URL: http://node1.mydomain.com:8529

    nodes:
    # list all your nodes and their public IPs here
    hosts:
        node1.mydomain.com:
        NODE_ID: 0 # the first BP (collator) node must have node ID 0
        HOST_PUBLIC_IP: 1.1.1.1
        node2.mydomain.com:
        NODE_ID: 1 # node IDs must be different for each node, and, preferably, be sequential
        HOST_PUBLIC_IP: 2.2.2.2
        node3.mydomain.com:
        NODE_ID: 2
        HOST_PUBLIC_IP: 3.3.3.3
        node4.mydomain.com:
        NODE_ID: 3
        HOST_PUBLIC_IP: 4.4.4.4
        node5.mydomain.com:
        NODE_ID: 4
        HOST_PUBLIC_IP: 5.5.5.5
    ```


### **Deploying docker on servers**


To install the necessary `docker` and `docker compose` plugins on the servers, follow these steps:

Install the `docker` role from Ansible galaxy:

```bash
ansible-galaxy role install geerlingguy.docker
```

Run the `ensure-docker` playbook to make sure that the necessary software is installed:

```bash
ansible-playbook -i inventory.yml ensure-docker.yml
```


### **Preparing the host configuration**


For reliable behavior of nodes, it is needed to run the `prepare-hosts` playbook to adjust some parameters on the servers:

```bash
ansible-playbook -i inventory.yml prepare-hosts.yml
```

It is important to note that it should be run after installing docker, because it adjusts some limits of the service.


### **Deploy front services on the BP (collator)** (node 1)


To make sure that no entities are missed on the front, first, front services must be deployed before starting the network.

To do that, use the `deploy-front` playbook:

```bash
ansible-playbook -i inventory.yml deploy-front.yml
```

!!! info

    Later, if necessary to clean the data on front, you can use `redeploy-front` playbook.


### **Deploying Caddy (or any other reverse-proxy)**


To provide straightforward secure access to endpoint and explorer, it is needed to deploy a revere proxy with certificate management.

The easiest way is to use `Caddy`, and it is provided as a ready for deployment playbook `deploy-caddy`.

```bash
ansible-playbook -i inventory.yml deploy-caddy.yml
```

!!! warning "Important"

    It uses `ackinacki-net` created by `deploy-front`, therefore, it must be executed after previous step.


Alternatively, you can deploy any other reverse proxy with certificate management you like.


### **Deploying and starting the network itself**


Before doing this step you must [**generate the BLS-keys**](deploy_network.md#generating-bls-keys) for validators and put them into `files` directory.

That is, the following files must be present in `files` directory (where `N` is number of nodes):

```
blockchain.conf.json
bls_publics.keys.json
validator0.keys.json
validator0_bls.keys.json
...
validatorN-1.keys.json
validatorN-1_bls.keys.json
```

Then you can deploy nodes and start the network (make sure your front is up and running!) using the following playbook:

```bash
ansible-playbook -i inventory.yml start-nodes.yml
```

!!! note

    Please note that node compilation may take a significant amount of time, even if it looks like the progress froze.


In case in future you need to stop the nodes you can use `stop-nodes` playbook, or `clean-nodes` to stop and delete data.


### **Post installation considerations**


#### **Setup firewall ports on front server**


For security reasons it is reasonable to restrict ports 8080 (nginx) and 8529 (arangodb) on the front server.

Just make sure that access from docker containers is maintained, otherwise things may break.
