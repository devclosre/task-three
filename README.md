# Task3: Using Ansible update the Home page of the Nginx server from "Hello World" to "Hello World from Ansible"
    1. In the Task, by using terraform we have created another server which acts as a Ansible Control Machine.
       

    2. We are considering Nginx server in ASG from Task1 as Node machine to Ansible Control Machine.
       We need to setup Passwordless Authentication between Ansible server and Nginx server, but by default AWS does not support
       Password Authentication, so we have to enable it on both the machine.
    3. First create a user called "devops", set a password and give him sudo permissions by going into visudo.
       ![image](https://github.com/devclosre/task-three/assets/143948725/ca1d0ac3-6589-4692-9bfc-1fd0c44adfa9)


    4. Next step would be enable Password Authentication and PubkeyAuthentication from "/etc/ssh/sshd_config" 
       ![image](https://github.com/devclosre/task-three/assets/143948725/d7a443d5-e981-4aa6-89d4-a91530e714f9)

       ![image](https://github.com/devclosre/task-three/assets/143948725/e34cb56d-182b-4a5d-b2eb-926fc2a241b6)


       Once the changes are done reload sshd service.
       ![image](https://github.com/devclosre/task-three/assets/143948725/d713cae6-bcff-408c-be32-2227963debf6)


    6. Now create a key pair using "ssh-keygen" and the keys will be store in "~/.ssh/id_rsa and id_rsa.pub"
       ![image](https://github.com/devclosre/task-three/assets/143948725/7c21b59f-5ba7-46a2-b049-d0efdbcb9870)
       

    7. Using "ssh-copy-id" copy the public key to Nginx server which is added as a host in the Ansible Control Machine
       Inventory file - "/etc/ansible/hosts". As the public key is copied to the Nginx server as the Passwordless Authentication
       is set between the Ansible Control Machine and Nginx server.

    8. Now we can see the Nginx server is still serving "Hello World"
       ![image](https://github.com/devclosre/task-three/assets/143948725/d07cd305-b98f-4897-b27b-abe4b4667a97)


    9. For testing the connection between both the machine, we do a basic ping using adhoc command:
       ![image](https://github.com/devclosre/task-three/assets/143948725/0dc0248c-e682-4433-927e-9fcb372b52fc)


    10. Now with update_nginx.yml and index.html, we will use the following command to update the Nginx server from "Hello World" to
        "Hello World to Ansible"
        
       ![image](https://github.com/devclosre/task-three/assets/143948725/c2ca2e4b-3c0c-47bc-a1ba-c15b93f915fe)

       ![image](https://github.com/devclosre/task-three/assets/143948725/5afd97e3-526e-4dbd-862b-b17e2820ecef)
       


    11. Upon successful execution of the playbook we can now see "Hello World from Ansible" as the Nginx server is reloaded using hanlders task,
        which gets notified by some copy task.
        
        ![image](https://github.com/devclosre/task-three/assets/143948725/bf6e2b74-ea2b-4707-9680-b10c6e9367eb)

