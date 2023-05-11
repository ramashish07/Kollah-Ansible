
#  KOLLA ANSIBLE OPENSTACK

The Kolla Ansible is a deliverable project separated from Kolla project. Kolla Ansible deploys OpenStack services and infrastructure components in Docker containers.



## Install dependencies
1. Updating the package index 
 ``` sudo apt update ```    

2.   Install Python build dependencies:
```sudo apt install git python3-dev libffi-dev gcc libssl-dev```
 ### Install dependencies for the virtual environment¶

 1. Install the virtual environment dependencies.
 ``` sudo apt install python3-venv ```

 2.  Create a virtual environment and activate it:
  ``` python3 -m venv /home/myproject/env```  
    ``` source /home/myproject/env/bin/activate```

3. Ensure the latest version of pip is installed:
```pip install -U pip ```    

4. Install Ansible. 
```pip install 'ansible>=4,<6' ```

## Install Kolla-ansible
1. Install kolla-ansible and its dependencies using pip.
``` pip install git+https://opendev.org/openstack/kolla-ansible@master```  

2. Create the /etc/kolla directory.
```sudo mkdir -p /etc/kolla ```  
```sudo chown $USER:$USER /etc/kolla```

3. Copy globals.yml and passwords.yml to /etc/kolla directory.
``` cp -r /home/myproject/env/share/kolla-ansible/etc_examples/kolla/* /etc/kolla```

4. Copy all-in-one inventory file to the current directory.
```cp home/myproject/env/share/kolla-ansible/ansible/inventory/all-in-one```

## Install Ansible Galaxy requirements
Install Ansible Galaxy dependencies:

``` kolla-ansible install-deps```

## Prepare initial configuration

### Inventory
The next step is to prepare our inventory file. An inventory is an Ansible file where we specify hosts and the groups that they belong to. We can use this to define node roles and access credentials.

Kolla Ansible comes with all-in-one and multinode example inventory files. The difference between them is that the former is ready for deploying single node OpenStack on localhost. In this guide we will show the all-in-one installation.

### Kolla passwords
Passwords used in our deployment are stored in /etc/kolla/passwords.yml file. All passwords are blank in this file and have to be filled either manually or by running random password generator:

``` kolla-genpwd```  

### Kolla globals.yml¶

``` kolla_base_distro="rocky"```  
```openstack_tag_suffix= "-aarch64"```  
```network_interface: "eth0"```  
``` neutron_external_interface: "eth1"```   
```kolla_internal_vip_address: "10.1.0.250"```

## Deployment 
1. Bootstrap servers with kolla deploy dependencies:
``` kolla-ansible -i ./all-in-one bootstrap-servers```

2. Do pre-deployment checks for hosts:
``` kolla-ansible -i ./all-in-one prechecks```  

3. kolla-ansible -i ./all-in-one deploy
```kolla-ansible -i ./all-in-one deploy```

## Using openstack

1. Install the OpenStack CLI client:
```pip install python-openstackclient -c https://releases.openstack.org/constraints/upper/master```

2. OpenStack requires a clouds.yaml file where credentials for the admin user are set. To generate this file:
```kolla-ansible post-deploy```

3. Depending on how you installed Kolla Ansible, there is a script that will create example networks, images, and so on.
```/path/to/venv/share/kolla-ansible/init-runonce```


![image](https://github.com/ramashish07/Kollah-Ansible/assets/91429764/9f0ca36b-8030-4c94-8382-c950117f1432)
![image](https://github.com/ramashish07/Kollah-Ansible/assets/91429764/5cf6e0c2-febe-42b6-b511-0b8d2dae1ca7)
![image](https://github.com/ramashish07/Kollah-Ansible/assets/91429764/dbd6ca14-977e-499b-8024-8ae6b64d6888)
![image](https://github.com/ramashish07/Kollah-Ansible/assets/91429764/272dcf51-6afe-4932-b6a9-244dfff51202)
![image](https://github.com/ramashish07/Kollah-Ansible/assets/91429764/d37cd19e-d4c4-47c4-9abc-9610eca5bc75)



## Group 11

- Ramashish Pandey -IEC2020095
- Vaibhav Goel     -IEC2020086
- Dhruv Bansal     -IEC2020084
- Harshil Gupta    -IEC2020082
- Shyam Kumar      -MWC2020009
- Nampali Dilip    -IIT2020060
