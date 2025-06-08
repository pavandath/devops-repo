## After successfully installing docker run:
    - docker run helloworld

- Now in your server there are two things:
    - **docker client** and **docker daemon**
    - whenever docker client runs the above command
    - docker daemon simply maintans containers and images, in the above command helloworld is an image whenever we run that command it creates a container
    - daemon checks for the image is there locally, if not then it will pull the image from registry (docker hub) and if we dont specify the version it will pull the latest image and then it will run container
    - To check images 
        - docker images # list of images that are available in out machine
    - To check containers
        - docker ps # list of containers running in the machine
    - To check stopped containers
        - docker ps -a
    
**Note:** once the process ends in a container the it life ends, it will running only when a process is running