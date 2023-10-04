# Deploying a React Web App using Docker Swarm on AWS
# DevOps-Project-5
<br></br>

# Project Blog link :-
<br></br>

# Project Overview :-
<br></br>

# Project Steps :-
- Create 2 ec2 instance :
Deploying a React Web App using Docker Swarm on AWS    : AWS Linux-2, t2 micro
<br></br>
![image](https://github.com/rutikdevops/DevOps-Project-6/assets/109506158/8ebe0cd5-f321-46b4-bfb3-5e2ac6a7f984)
<br></br>
- Goto Security-> security group-> Edit inbound rules-> Add rule-> choose All Traffic
<br></br>
![image](https://github.com/rutikdevops/DevOps-Project-5/assets/109506158/c33dcb98-c446-4d35-b9e0-b24cfedbb1b7)
<br></br>


# 1. Install and Configure the Docker on both instances :-
```bash
ubuntu
sudo su
apt update -y
apt install docker.io -y
hostnamectl set-hostname docker
bash
docker ps
whoami
chown $USER /var/run/docker.sock
```
<br></br>

# 2. Clone the Github code :-
```bash
git clone https://github.com/LondheShubham153/two-tier-flask-app.git
cd two-tier-flask-app
```


# 3. Initialize Swarm on Swarm Master Instance :-
- Access the "Swarm Manager" node and initiate the Swarm by running the following command:-
```bash
docker swarm init     # This command initializes an empty Swarm.
```

# 4. Add Workers to the Swarm :-
- After initializing the Swarm on the "swarm-master" node, a key will be generated. You need to copy and run this key on the other server (Swarm-worker). This step adds both machines as workers to the Swarm.

# 5 : Check Swarm Node Status :-
- To verify the status of all nodes in the Swarm, run the following command on the manager node:
```bash
docker node ls       # This command will display information about all the nodes in the Swarm.
```

# 6: Create a Docker Service 🛠️
- On the Swarm Manager node, create a Docker service using the following command:
```bash
docker service create --name react-app-service --replicas=2 --publish 3000:3000 rutikdevops/reactapp1
```
- This command creates a service named "react-app-service" with three replicas, publishing port 3000.

![image](https://github.com/rutikdevops/DevOps-Project-6/assets/109506158/40fca8db-a232-4cbe-9b37-ea77cc2f7a6a)

# 7: List Docker Services :-
- To list the Docker services running in the Swarm, use the following command:-
```bash
sudo docker service ls     # This will display a list of services, including the one you just created.
```

# Step 8: Verify Containers :-
- The service you created will deploy containers on the Master and worker nodes. To check if containers are running on the master node, execute:
```bash
docker ps                 # You should see containers related to your service.
```

# 9: Access the Web App 🌐 :-
- Now, your web app service is running on all three nodes. To access it, grab the IP address of any of the nodes followed by port 3000, like this:
```bash
ec2-3-111-170-216.ap-south-1.compute.amazonaws.com:3000
```
![image](https://github.com/rutikdevops/DevOps-Project-6/assets/109506158/bdef3fff-de7d-472f-be62-27b0ab034278)
- You should be able to access your web application through this URL.


