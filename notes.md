The "volumes" section is where we specify any data that we want to persist outside of the container. In this case, we're mapping a local directory called "data" (which will be created in the same directory as this docker-compose.yml file) to the /data directory inside the

# Useful commands to manage the container:
# To start the container: docker-compose up -d
# To stop the container: docker-compose down
# To view logs: docker-compose logs -f vaultwarden
# Note: Make sure to replace "your_admin_token_here" with a secure token of your choice. This token will be used to access the admin panel of Vaultwarden, so it should be something unique and not easily guessable.

#What to remember when coding with YAML:
#1. Indentation is crucial in YAML. Use spaces, not tabs, and be consistent
#2. Key-value pairs are defined with a colon (:) followed by a space
#3. Lists are defined with a dash (-) followed by a space
#4. Comments can be added with a hash (#) and are ignored by the parser

#Notes:
#version: '3.8'
# Docker Compose file for Vaultwarden (Bitwarden Server)
#services:
# Start section to define the container for Vaultwarden
# A "service" is basically one app/container that we want to run. In this case, it's the Vaultwarden server.
# Later, bigger projects might have multiple services (like a web server, a database, etc.), but here we just have one.
  #vaultwarden:
  # Name of my service. This is just a label we use to refer to this container in our Docker Compose file. You can name it anything you like, but "vaultwarden" makes it clear what this service is for.
    #image: vaultwarden/server:latest
    #This line tells Docker which image to use for this container. "vaultwarden/server:latest" means we want to use the latest version of the Vaultwarden server image from Docker Hub. Docker will automatically download this image if it's not already on your machine.
    # vaultwarden/server is the name of the image, and :latest is a tag that specifies we want the latest version of that image. If you wanted a specific version, you could replace "latest" with something like "1.30.0" or whatever version you want to use.
    # pinning the version is a good practice for production environments to ensure stability, but for testing or personal use, using "latest" is often fine.
    #container_name: vaultwarden
    # This line gives a specific name to the container when it runs. By default, Docker would generate a random name for the container, but by specifying "container_name: vaultwarden", we can easily refer to this container by name when we want to manage it (like viewing logs or stopping it).
    #restart: unless-stopped
    # This line tells Docker to automatically restart the container if it crashes or if the Docker daemon restarts. "unless-stopped" means that the container will keep restarting unless you explicitly stop it. This is useful for ensuring that your Vaultwarden server stays up and running without manual intervention.
    #ports:
      #- "127.0.0.1:8082:80"
      # This line maps port 80 inside the container (where the Vaultwarden server listens) to port 8082 on your local machine, but only on the localhost interface (127.0.0.1). This means you can access the Vaultwarden web interface by going to http://localhost:8082 in your web browser, but it won't be accessible from other devices on your network, which adds a layer of security.
    #environment:
    # This section is where we set environment variables that the Vaultwarden server uses to configure itself. These variables control various aspects of how the server operates.
      #WEBSOCKET_ENABLED: "true"
      # This variable enables WebSocket support in Vaultwarden, which allows for real-time updates in the web interface. When set to "true", it means that the server will use WebSockets to push updates to the client without needing the user to refresh the page.
      #SIGNUPS_ALLOWED: "true"
      # This variable allows new users to sign up for accounts on the Vaultwarden server. When set to "true", anyone can create an account. If you want to restrict account creation (for example, if you're running this in a more private environment), you could set this to "false".
      #ADMIN_TOKEN: "your_admin_token_here"  
      # This variable sets the admin token for accessing the admin panel of Vaultwarden. You should replace "your_admin_token_here" with a secure token of your choice. This token is required to log in to the admin panel, where you can manage users, view logs, and perform other administrative tasks. Make sure to choose a strong, unique token to prevent unauthorized access to your admin panel.
    #volumes:
    # This section is where we define any volumes that we want to use for this container. Volumes are a way to persist data outside of the container's filesystem, which is important because if the container is deleted, any data stored inside it would be lost. By using a volume, we can ensure that our data (like user accounts and vaults) is saved even if we need to recreate the container.
      #- ./data:/data
      # This line maps a local directory called "data" (which will be created in the same directory as this docker-compose.yml file) to the /data directory inside the container. The Vaultwarden server uses the /data directory to store all of its data, so by mapping it to a local directory, we can easily access and back up our data from outside the container.


Docker container try 1
 - Forget to add in the ADMIN TOKEN so create an example docker compose and a personal docker compose, added the admin token to the non-example on and then added the non-exmaple docker compose to the .gitignore

Docker container try 2
 - right click the docker i want to get up, Executed task: docker-compose -f 'docker-compose.yml' up -d --build 
 - failed and spitted out 
 *  The terminal process "/bin/bash '-c', 'docker-compose -f 'docker-compose.yml' up -d --build'" terminated with exit code: 1. 
 *  Terminal will be reused by tasks, press any key to close it. 

 - This means its trying to connect to docker via a Unix socket (idk what that is learn later) but is being denied access due to insufficient permissions
 - Docker socket owend by the docker group and the current user (azureuser) isn't member of that groups
 How to fix: run with sudo command (duhhhh)

docker container try 3 
 - it worked when i used sudo docker-compose -f docker-compose.yml up -d --build instead of docker-compose -f docker-compose.yml up -d --build
