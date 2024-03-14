# B9IS121_2324_TMD2_NETWORKS_SYSTEMS_ADM
This repository is for completing the class assignments for B9IS121 NETWORKS AND SYSTEMS ADMINISTRATION (B9IS121_2324_TMD2)

How it works
Note: the instructions based on how it work on your Ubuntu PC
1. Clone the repository to your local PC using 'git clone'
2. Update the main using 'git pull' command. 
3. Prepare the host PCs deployment environment
    a. install python 3 (sudo apt install python3)
    b. install python package manager pip (sudo apt install python3-pip)
    c. install ansible (pip3 install ansible), try sudo apt install ansible if this not work
4. Execute the ansible script, following will be printed to the console.
    # ansible-playbook docker_deploy.yml.yml 
    PLAY [Deploy Apache Docker Container] **********************************************

    TASK [Gathering Facts] **********************************************
    ok: [localhost]

    TASK [Install Docker Python package] **********************************************
    ok: [localhost]

    TASK [Set up container to run on 172.168.10.0/30 subnet ******************************************
    ok: [localhost]

    TASK [Pull Apache Docker image] **********************************************
    ok: [localhost]

    TASK [Define list of container configurations] **********************************************
    ok: [localhost]

    TASK [deploy an Apache Docker container] **********************************************
    ok: [localhost] => (item={'name': '20024471_B9IS121-container-1', 'image': 'httpd:latest', 'volumes': ['/home/nishshanka/Documents/20024471_B9IS121_2324_TMD2_NETWORKS_SYSTEMS_ADM/myweb:/usr/local/apache2/htdocs'], 'ports': ['8080:80'], 'networks': [{'name': '20024471_B9IS121-network', 'ipv4_address': '172.168.10.2'}], 'networks_cli_compatible': True, 'container_default_behavior': 'compatibility', 'network_mode': 'default'})

    PLAY RECAP **********************************************
    localhost                  : ok=6    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
5. Check the existance of the Docker containers using docker ps command
    # docker ps
    CONTAINER ID   IMAGE          COMMAND              CREATED          STATUS          PORTS                  NAMES
    a3e08c9521df   httpd:latest   "httpd-foreground"   55 minutes ago   Up 19 minutes   0.0.0.0:8080->80/tcp   20024471_B9IS121-container-1
6. Also check the creation of docker network with 'docker network ls'
    # docker network ls
    NETWORK ID     NAME                       DRIVER    SCOPE
    34750191842e   20024471_B9IS121-network   bridge    local
    e162643cda63   bridge                     bridge    local
    5863b7b50d0d   docker_gwbridge            bridge    local
    71fe44244caa   host                       host      local
    iiwqbusc80xe   ingress                    overlay   swarm
    3d662baa4877   none                       null      local

    here, docker_gwbridge network is created automatically and the second IP is assign to it.
7. Try to ping the bridge IP and the containers IP
    # ping 172.168.10.2
    PING 172.168.10.2 (172.168.10.2) 56(84) bytes of data.
    64 bytes from 172.168.10.2: icmp_seq=1 ttl=64 time=0.083 ms
    64 bytes from 172.168.10.2: icmp_seq=2 ttl=64 time=0.126 ms

    # ping 172.168.10.2
    PING 172.168.10.2 (172.168.10.2) 56(84) bytes of data.
    64 bytes from 172.168.10.2: icmp_seq=1 ttl=64 time=0.083 ms
    64 bytes from 172.168.10.2: icmp_seq=2 ttl=64 time=0.126 ms
8. Open web browser and reach http://172.168.10.2/index.html to access the apache web site on the   container.