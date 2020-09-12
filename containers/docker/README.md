# Starting the docker daemon
On Linux you must first ensure that the docker daemon is running. You can do that by e.g. running `dockerd` manually with root privileges in a separate shell session.

# First steps
You can ensure docker is running by executing the command `docker ps -a`. This will list all container containers currently existing.

For the first container to test the working system you can run `docker run hello-world`. This will create a container from the hello-world image, which is downloaded from the docker repository.
It should print out a Hello World message plus some additional information. Then you're ready to get started using docker.

# 
