# B9IS121_2324_TMD2_NETWORKS_SYSTEMS_ADM
This repository is for completing the class assignments for B9IS121 NETWORKS AND SYSTEMS ADMINISTRATION (B9IS121_2324_TMD2)

Task:
Automated Container deployment and Administration

list of files:
├── ansible.cfg                 # Ansible config file
├── DockerConnectivity.jpg      # Docker Connectivity Diagram
├── docker_deploy.yml           # Ansible script
├── inventory.ini               # inventory file
├── myweb                       # Web site
│   ├── css
│   │   └── main-css.css
│   └── index.html
├── output.log                  # console output for ansible script execution 
└── README.md                   # GIT repo README file


How it works
Note: the instructions based on how it work on your Ubuntu PC
1. Clone the repository to your local PC using 'git clone'. this is the control PC for executing the ansible script.
2. Update the main branch using 'git pull' command. 
3. Prepare the Control PCs deployment environment
    a. install python 3 (sudo apt install python3)
    b. install python package manager pip (sudo apt install python3-pip)
    c. install ansible (pip3 install ansible), try sudo apt install ansible if this not work
    d. Launch an ubuntu virtual machine and get the IP address of it. 
    e. Update inventory.ini file with Virtual Machine's IP address and the credentials for following   line
        host1 ansible_host=<IP Address> ansible_user=<userName> ansible_password=<password> 
4. Execute the ansible script with -i (to specify the inventory), --ask-pass(to enter the host Ubuntu VM password) and --ask-become-pass(to enable the docker execution rights), refer to the output.log file for the console output for the execution.
    # ansible-playbook -i inventory.ini docker_deploy.yml --ask-pass --ask-become-pass
5. Check the existance of the Docker containers using docker ps command. Logon to the virtual machine and open the terminal.
    # docker ps
    CONTAINER ID   IMAGE          COMMAND              CREATED          STATUS          PORTS                  NAMES
    2ca13c3e2c6e   httpd:latest   "httpd-foreground"   19 minutes ago   Up 19 minutes   0.0.0.0:8080->80/tcp   20024471_B9IS121-container-1

6. Also check the creation of docker network with 'docker network ls'
    # docker network ls
    NETWORK ID     NAME                       DRIVER    SCOPE
    b74025a88473   20024471_B9IS121-network   bridge    local
    76529ccf4222   bridge                     bridge    local
    f7dabdbe28b7   host                       host      local
    ac38c1af758c   none                       null      local
    
7. Try to ping the bridge IP and the containers IP
    # ping 172.168.10.2
    PING 172.168.10.2 (172.168.10.2) 56(84) bytes of data.
    64 bytes from 172.168.10.2: icmp_seq=1 ttl=64 time=0.083 ms
    64 bytes from 172.168.10.2: icmp_seq=2 ttl=64 time=0.126 ms

    # ping 172.168.10.2
    PING 172.168.10.2 (172.168.10.2) 56(84) bytes of data.
    64 bytes from 172.168.10.2: icmp_seq=1 ttl=64 time=0.083 ms
    64 bytes from 172.168.10.2: icmp_seq=2 ttl=64 time=0.126 ms

8. Open web browser and enter URL http://<Virtual machine IP>:<8080>/myweb/ (e.g. http://192.168.122.192:8080/myweb/) or hhttp://<Virtual machine IP>:<8080>/myweb/index.html to access the web site on the container.

References:
https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html#playbook-syntax
https://docs.ansible.com/ansible/2.9/modules/docker_network_module.html#parameter-ipam_config
https://docs.ansible.com/ansible/2.9/modules/docker_network_module.html
https://ankush-chavan.medium.com/configure-docker-containers-using-ansible-79fa460a62b4
https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html
