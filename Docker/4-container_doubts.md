## Difference between -it and exec -it
- In order to interact with the container while creation we use -it
- whereas, in order to connect to a running container we use exec -it 
    - docker exec  wonderful_thompson hostname -i
        172.17.0.2  
    -  docker exec  wonderful_thompson /bin/bash
      
## Difference between exec and attach

  - This will run the command in the running container but in order to interact with the container
    - docker exec -it wonderful_thompson
    - But here in container while you type exit it don't stop the container 
    - Why means exec tells that it will attach to the container secondary process not to the primary process, so when we use exit
    that secondary process is exited not primary process so container won't stop 
    - Now,
    - docker attach <container name/id>
    - and type exit it will stop the conatainer as well
    - So, docker attach by default will connect to the primary process of the container 
    - attach only works when we are starting a container with -it command

### docker run -it ubuntu
➤ Creates a new container from the Ubuntu image, and starts a new shell as the primary process.

### docker attach <container>
➤ Reconnects to the shell (primary process) of an already running container that was started with -it.


| Command                              | Purpose                                                                             |
| ------------------------------------ | ----------------------------------------------------------------------------------- |
| `docker run -it ubuntu`              | Start a **new container** with interactive access                                   |
| `docker attach myubuntu`             | Reconnect to the **original terminal** of the running container                     |
| `docker exec -it myubuntu /bin/bash` | Start a **new shell** inside the running container without touching the primary one |


