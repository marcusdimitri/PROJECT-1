# PROJECT-1
The files created in this project were used to configure this network.
![alt text](https://github.com/marcusdimitri/PROJECT-1/blob/main/Diagrams/UNIT%2012.png)



## Configuration of the machines.
| Machine       | Purpose     | IP     |
| ------------- |:-----------:| -----: | 
| ELK           |  Log Server |10.2.0.4|
| Web 1         | Docker-DVWA |10.0.0.5|
| Web 2         | Docker-DVWA |10.0.0.6| 
| JBOX          | Ansible     |10.0.0.4|






## Configuration of the ELK machine.
Ansible was used to automatically configure the ELK machine. This was done was done through playbooks that executes the following task. It installs docker, pip3, and the docker module.
### DOCKER 
```
---
- name: Configure Elk VM with Docker
  hosts: elk
  remote_user: ansible
  become: true
  tasks:
    # Use apt module
    - name: Install docker.io
      apt:
        update_cache: yes
        force_apt_get: yes
        name: docker.io
        state: present

      # Use apt module
    - name: Install python3-pip
      apt:
        force_apt_get: yes
        name: python3-pip
        state: present

      # Use pip module (It will default to pip3)
    - name: Install Docker module
      pip:
        name: docker
        state: present

    - name: Use more memory
      sysctl:
        name: vm.max_map_count
        value: "262144"
        state: present
        reload: yes
      # Use docker_container module
    - name: download and launch a docker elk container
      docker_container:
        name: elk
        image: sebp/elk:761
        state: started
        restart_policy: always
        published_ports:
          - 5601:5601
          - 9200:9200
          - 5044:5044              
```
  ## Playbooks
  
 [ELK](https://github.com/marcusdimitri/PROJECT-1/blob/main/ansible/elk.yml)
 
 [FILEBEAT PLAYBOOK](https://github.com/marcusdimitri/PROJECT-1/blob/main/ansible/filebeat_playbook.yml)
 
 [PLAYBOOK]( https://github.com/marcusdimitri/PROJECT-1/blob/main/ansible/playbook1.yml)    
 
