## Docker Image Fundamentals

- **Layered Structure**: Docker images are made up of stacked, read-only layers.
- **Template Nature**: They serve as read-only templates for creating containers.
- **Base & Custom Layers**: You typically start with a base image and add your application's specific layers on top.
- **Layer Caching**: Docker uses caching; if different image versions share layers, those layers aren't re-downloaded or rebuilt, saving time and bandwidth.
- **Immutability**: Once built, a Docker image cannot be modified. Any changes require building a new image.
- **Container's Writable Layer**: When a container is created, a read/write layer is added on top of the image's read-only layers. All changes made within the running container occur in this writable layer.

## Creating image thorugh commit way
**Never tell about this in interview**

**Note:** While this method works, it's not recommended for standard development and is best avoided in interviews. It's more suited for quick experiments or specific automation needs.
- This method creates a new image directly from the current state of a running container. Essentially, it "snapshots" the container.
- It is simply creating an image from a container, basically the container don't come with all the resources so we interact with it modify and from it we create an image
- Simply create a container using ubuntu image (docker run -it ubuntu)
- Run **apt update -y && apt install iputils-ping**
- Now to create an image from a container run
    -  docker container commit 6f14589db581    ubuntu:custom
                              <container-id>  <image name:tag>
                                 <or name>
## docker export 

**docker export custom > ubuntucustom.tar**
              <id/name>
- This command simply creates a tar file of the container
- you can share this tar file directly but it doesn't create a container
- So Now:
- To create the image from it use **import**

**docker import - image-name:v1 < ubuntucustom.tar**

- Similarly
    - **docker save** > creates a tar file from image
    - **docker load** > loading a image from tar file
## Docker push and pull into registry
- registry url format
            docker.i/username/repositoryname:tagname
- In local machine we can save the image name whatever we want but where as while pushing into registry we need to follow the order:
    - username/repositoryname:tagname

- To rename that image use
        **docker tag ubuntu:custom pavandath510/ubuntunewcustom:v1**

- Now run 
    - docker login -u <username>
    - docker push pavandath510/ubuntunewcustom:v1
