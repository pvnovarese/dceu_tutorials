Understanding Docker Volumes

**Objective**: The goal of this lab is help you gain an understanding of Docker’s use of volumes. By the end of the lab you should be able to:

* Implement a Docker volume via the Docker client

* Understand how Docker represents volumes in the file system

* Delete a Docker volume

* Map a host directory to a Docker volume

* Use a volume to share data between containers

**Time**: It’s estimated that this lab will take XX minutes to complete

# What are Docker data volumes?

A data volume is a specially-designated directory within one or more containers that bypasses Docker’s storage driver and interacts directly with the host file system. Data volumes provide several useful features for persistent or shared data:

* Volumes are initialized when a container is created. If the container’s base image contains data at the specified mount point, that existing data is copied into the new volume upon volume initialization.

* Data volumes can be shared and reused among containers.

* Changes to a data volume are made directly to the host filesystem (vs. going through the storage driver)

* Changes to a data volume will not be included when you update an image.

* Data volumes persist even if the container itself is deleted.

Data volumes are designed to persist data, independent of the container’s lifecycle. Docker therefore never automatically deletes volumes when you remove a container, nor will it "garbage collect" volumes that are no longer referenced by a container.

# Log into your Docker host

1. SSH into your Docker host with the supplied credentials

# Implementing a volume via the Docker client

1. Pull down the official Nginx image

2. Create a new  volume named /barcelona



**Note***: Your new volume will be created on the host in the**/var/lib/docker/volumes** **directory*

3. Ensure your volume was created by using docker volume ls to list the volumes on your Docker host

4. Instantiate a Docker container with our barcelona volume mapped to /barcelona in the container, and log into the shell

5. **_Note_***: You are now working within the shell of your running container

6. Create a file in that directory

7. List the directory contents to make sure the file exists

8. Exit the container but leave it running by hitting Ctrl+P (at the same time) and then hitting Ctrl+Q (at the same time)

# Understand how Docker represents volume data in the file system

As mentioned above, Docker manages volumes outside of the storage driver that it uses to manage the layers of a given container. This allows for data persistence(the volume is not destroyed when the container is destroyed).

1. You can use  docker volume inspect to learn details about about a given volume. In this case our barcelona volume

2. In order to examine the contents of the directory, you’ll need to elevate your user privileges:

3. Change to the volumes data directory in the host filesystem

4. List the contents of the directory

5. Create a new file

6. Ensure both file.txt and file2.txt exist in the directory

7. Log back into the shell of the running container using the docker exec command

8. **_Note_***: You are now working within the shell of your running container*

9. Exit the container, and return to your docker host

# Deleting a volume

By default, when you destroy a container Docker does not remove any volumes associated with the container. You can delete a given volume with the docker volume rm command

1. Stop the container we have been working with previously

2. Remove the container.

3. Ensure the volume we were working with still exists

4. Elevate your privileges

5. List the contents of the volume directory to see that the two files are still there

6. Exit superuser

7. Remove the volume

8. Ensure the volume was removed

# Map a host directory to a Docker volume

In the previous exercises we were able to manipulate data files in a Docker volume via the host file system,. However, it was a bit cumbersome: we had to learn the mount point via docker volume inspect, and elevate our privileges to create a new file. In practice, this is impractical.

1. Create a www subdirectory on your Docker host

2. Change into your www directory

3. Use the following command to create an index.html file with some content.

**Note***: Be sure to use single quotes in the command above.*

4. Instantiate an Nginx container that maps the ~/www directory on the host to /usr/share/nginx/html in the running container

5. Use the browser on your laptop to navigate to navigate to the newly created website at http://<docker host>:8001/

6. Return to your Docker host’s terminal window, and update the HTML of your website with the following command:

7. Reload the website in your browser, and notice how the change to the local filesystem is immediately reflected by the running Nginx container.

# Use a volume to share data between containers

You can also use volumes to share data between containers. For instance, one container could be writing data to a log file, and a second container could be reading that data and providing a graphical interpretation.

In our example we’ll simply create a new file from one container in a directory that is mounted point for a named container, and then list the directory from another container.

1. Create a new named volume

2. Create a new container (named foo), mount the named volume to the /foo directory, and log into the shell

3. Create a new file in the /foo directory (which is mapped to your shared-data volume)

4. Verify the content of your newly created file

5. Exit the container, but leave it running by typing Ctrl-P and then Ctrl-Q

6. Create a second container (named bar), mount the previously created named volume (shared-data) to the /bar directory, and log into the shell

7. Create a new file in the /foo directory (which is mapped to your shared-data volume)

8. Verify the content of your newly created file

9. Exit this container

10. Log back into the shell of the original container using the docker exec command

11. Check to see if the changes you made in the bar container are reflected in this container

12. Exit this container

# Conclusion

In this lab we learned the basics of Docker volumes. We created a new Docker volume using the Docker client, and then explored the host file system to understand the relationship between the local file system and the mounted volume in the container. We then deleted our volume, and mapped a new volume to a specific directory on the host file system. Finally we looked at how you can share a volume between multiple containers.

Feel free to continue exploring Docker volumes.