Docker-compose is used for creating server and client services in Docker.
The main folder includes the docker-compose.yml file. It also has service and client folders in which a python file with thrift library, the modified challenge.thrift file and a Dockerfile for that service are.

To create the image of server and client, go to the main directory where the docker-compose file is and type:

```bash
docker-compose build
```

Two images are built for client and server. To run it together, type:
```bash
docker-compose up
```

To run each image separately, type:

```bash
docker run -it --network=host pythonengineerchallenge_server:latest python server.py
```

pythonengineerchallenge_client is the name of server image. It will be different in your machine if you change the name of main folder. This line of code prepares the server. Then, it is time for client container to be created. To do so, type:
```bash
docker run -it --network=host -p 9090 pythonengineerchallenge_client:latest python client.py
```
pythonengineerchallenge_client is the name of client image. 
At this point, you are asked to enter the first number, then enter. Then, you will ask for the second number. After entering, the result is printed.