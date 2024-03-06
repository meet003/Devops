-------------Docker-----------

# Docker Compose

//to start compose file
docker-compose up -d

//to stop compose file
docker-compose down -d



// file name : - docker-compose.ymal
version: "3.9"
services:
  frontend:
    container_name: "flowXpert"
    build : .
    ports:
      - 8000:8000
    volumes:
      - django_todo_volume:/app
  mysql_db:
    container_name: "flowXpert"
    image: mysql:5.7
    ports:
      - 3306:3306
    environment: 
      MYSQL_ROOT_PASSWORD: "TEST@123"
volumes:
  django_todo_volume:
   






# Docker volume

! To create Docker Volume --

cmd :- docker volume create --name django_todo_volume --opt type=none --opt device=/home/ubuntu/volumes/django-todo --opt o=bind

1. django_todo_volume : volume name
2. --opt device=/home/ubuntu/volumes/django-todo : current path were volumes is created


! To mount with container

cmd mein  while creating container :- --mount source=django_volume,target=/app

1. source=django_volume -- django_volume is volume name



# Docker File--------------------------


//Flask

# Use an official Python runtime as a parent image 
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed dependencies specified in requirements.txt
RUN apt-get update && apt-get install -y vim && \
    pip install --no-cache-dir -r requirements.txt

# Expose port 5000 to the outside world
EXPOSE 5005

# Define environment variable
ENV FLASK_APP=app.py

# Run app.py when the container launches
CMD ["flask", "run", "--host=0.0.0.0", "--port=5005"]

------------------------------------------------------------------------------------------------

# Doker swarm

-- first need to create more then 1 one instance
eg :- 
1. master server
2. worker server 
3. worker server and more.....


===In master node
*cmd* - docker swarm init


**To create service**

*cmd*:-  docker service create --name kiwikID-service --replicas 3 --publish 8001:8001 <image>
 note:- kiwikID-service is service name


 **Docker stack**
 docker stack deploy -c <meet.yaml> flowxpert
 note:- flowxpert is stack name

 --update running conatiner image

 *cmd*:- sudo docker sercive update --image <image-name>
 note:- image should in docker hun