# Deploying a React Web App using Docker Swarm on AWS
# DevOps-Project-5
<br></br>

# Project Blog link :-
<br></br>

# Project Overview :-
<br></br>

# Project Steps :-
# 1. Create 3 ec2 instance :
Deploying a React Web App using Docker Swarm on AWS    : AWS Linux-2, t2 micro
<br></br>
![image](https://github.com/rutikdevops/DevOps-Project-6/assets/109506158/60356d92-ce3c-46e4-95eb-a8eda3900c03)
<br></br>
- Goto Security-> security group-> Edit inbound rules-> Add rule-> choose All Traffic
<br></br>
![image](https://github.com/rutikdevops/DevOps-Project-5/assets/109506158/c33dcb98-c446-4d35-b9e0-b24cfedbb1b7)
<br></br>


# 2. Install and Configure the Docker on all the instances :-
```bash
ubuntu
sudo su
apt update -y
apt install docker.io -y
docker --version
systemctl enable docker
systemctl start docker
systemctl status docker
```
<br></br>

# 3. Initialize Swarm on Swarm Master Instance :-
- Access the "Swarm Manager" node and initiate the Swarm by running the following command :-
```bash
docker swarm init     # This command initializes an empty Swarm.
```

# 4. Add Workers to the Swarm :-
- After initializing the Swarm on the "swarm-master" node, a key will be generated. You need to copy and run this key on the other server (Swarm-worker). This step adds both machines as workers to the Swarm.

# 5. Check Swarm Node Status :-
- To verify the status of all nodes in the Swarm, run the following command on the manager node:
```bash
docker node ls       # This command will display information about all the nodes in the Swarm.
```
![image](https://github.com/rutikdevops/DevOps-Project-6/assets/109506158/192ec7c3-c027-46b3-a23c-bb02e42b0afb)


# 6. Clone the Github code on Master :-
```bash
git clone https://github.com/LondheShubham153/two-tier-flask-app.git
cd two-tier-flask-app
```
- Create Docker File :-
```bash
Vi Dockerfile1.dev
```

# 7. Create a docker image from Dockerfile :-
```bash
docker build -f Dockerfile.dev -t reactapp1 .
docker images
```

# 8. Create Docker Container from Docker Image :-
```bash
docker run -it -p 3000:3000 --name reactApp reactapp1
```
![image](https://github.com/rutikdevops/DevOps-Project-6/assets/109506158/80b6d103-a77f-4e88-9889-83b5a68f83fc)


- Now, The React App is Running on Swarm-Master Node :-

![image](https://github.com/rutikdevops/DevOps-Project-6/assets/109506158/992f95b9-deed-4776-95dc-3068e223c2fd)



# 9. Create a Docker Service 🛠️
- On the Swarm Manager node, create a Docker service using the following command:
```bash
docker service create --name react-app-service --replicas=2 --publish 3000:3000 reactapp1   # This command creates a service named "react-app-service" with three replicas, publishing port 3000.
```
- Now Your App is running on Swarm-Worker Node :-
![image](https://github.com/rutikdevops/DevOps-Project-6/assets/109506158/9267b46c-a7ef-4851-b8a8-6c38a41d5bbc)





# 10. List Docker Services :-
- To list the Docker services running in the Swarm, use the following command:-
```bash
sudo docker service ls     # This will display a list of services, including the one you just created.
```
![image](https://github.com/rutikdevops/DevOps-Project-6/assets/109506158/2aba5eeb-e568-4ae7-809f-3c0891a152d1)


# 11. Verify Containers :-
- The service you created will deploy containers on the Master and worker nodes. To check if containers are running on the master node, execute:
```bash
docker ps                 # You should see containers related to your service.
```



# 12. Push Docker Image to DockerHub :-
```bash
docker login
# Enter username & password
docker tag reactapp1 rutikdevops/reactapp1
docker images
docker push rutikdevops/reactapp1
```
![image](https://github.com/rutikdevops/DevOps-Project-6/assets/109506158/40fca8db-a232-4cbe-9b37-ea77cc2f7a6a)


# 13. Guest User pull this Docker image And deploy it on his own Machine :-
```bash
docker pull rutikdevops/reactapp1
docker images
docker run -it -p 3000:3000 --name rutik_reactapp rutikdevops/reactapp1
```
![image](https://github.com/rutikdevops/DevOps-Project-6/assets/109506158/5fc84731-a5d1-4d94-a425-9d1732c7e785)


# 14. Access the Web App 🌐 :-
- Now, your web app service is running on all three Instances. To access it, grab the IP address of any of the nodes followed by port 3000, like this:
```bash
ec2-3-111-170-216.ap-south-1.compute.amazonaws.com:3000
```
![image](https://github.com/rutikdevops/DevOps-Project-6/assets/109506158/bdef3fff-de7d-472f-be62-27b0ab034278)












