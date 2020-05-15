# Configuration in the Dockerfile

>### **Common steps:**

```
FROM python:3.6.1-alpine
RUN pip install flask
CMD ["python","app.py"]
COPY app.py /app.py
```

>* **FROM:** It is the start of every Dockerfile, it is followed with the base image you wanna use for your app.
>
>* **RUN:** The commmand after it is being used for set up the dependancies, such as install flask for a falsk application
>
>* **CMD:** CMD can only appear once in each Dockerfile, the commands inside will only run after you run the container
>
>* **COPY:** It will copy the file/dir that you need for your app to the layer of docker


# Scripts to run the app.py inside docker

>### **1. To build the Docker file:**
>* **-t** is the tag, to give the image a new tag name

    $ docker build -t hello-world .


>### **2. To run app.py in the new container:**

>* **-d** is --detach, which makes the container running in the background;
>
>* **-p** is --port, which maps the port 5000 in the container to the port 80 of the host server;
>
>* **--name** is to give a name for the container

    $ docker run -d -p 80:5000 --name hw hello-world

>### **3. To see logs of this container:**
> you can replace **hw** with the **container id** (no need to use the full id, number of chars to make it unique is enough)

    $ docker container logs hw

>### **4. To remove a container:**
> two ways can do this:
>* first stop the container

    $ docker stop hw

>* then you can either do

    $ docker rm hw

>* or you can

    $ docker system prune

>* and this will remove all stopped containers
>### **5. To remove an image:**

    $ docker rmi [img-tag1] [img-tag2] [...]

>### **6. Some check status commands:**
>* See all active/running containers

    $ docker container ls

>* or 

    $ docker ps

>* see all containers just add **-all**:

    $ docker ps -all

>* See all images in your machine:

    $ docker images

>### **7. To push a central registry**
> When you make sure the app is running good in docker, you may wanna save this image to a repo in docker-hub for future use, then first you can either login using the docker-desktop or you can

    $ docker login

> then tag the image to the folder and push it to your repo, the tag must be the same as your repo's name, and it will create a new tag for the same image.

    $ docker tag hello-world [account-id]/my-app
    $ docker push [account-id]/my-app
>### **8. Update your app**
> simply remove all containers and images then build a new image and run a container again.

> to update the repo:

    $ docker build -t [account-id]/my-app .
    $ docker push [account-id]/my-app