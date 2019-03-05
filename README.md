#  Load Balancer Prototype
A mini project made to implement concepts of client server architecture.
The distribution of load takes place based on the CPU usage of each worker nodes.
The client sends a number to the server and it receives the prime number which are smaller that the provided number.
Ex: 
Input: 100
Output: 97

Input: 6
Output: 5

#### Client
Client will request use for server's IP and connect to the server on port 7777.
After that the server can proceed to provide inputs. Type `done` when user is willing to quit the application.

#### Server
Server listens at port 2222 for the worker nodes to connect. Large number of worker nodes are supported at anytime, which makes this project highly scalable.
Server also listens on port 7777 for client requests. docker-compose will bind the localhost:7777 to server's 7777 port. Server needs no input from the user.

#### Worker
The worker node requests a connection from server at port 2222 and it's always listening on port 5555.
Following which server establishes a TCP connection to the workers on port 5555. Worker nodes need no input from the user.

## Installation

It requires `java`, `docker` and `docker-compose` to work. 
Please follow the installation process from the official documentation of all the dependencies.

Use `Dockerfile` in server and farm to build an image.

```bash
cd loadBalancer/Server/src
docker build -t "loadbalancer/server" .
```

Build Worker image:

```bash
cd loadBalancer/Worker/src
docker build -t "loadbalancer/worker" .
```

## How to use

Once images are created we will use docker-compose to turn up the server and the worker nodes

```bash
cd loadBalancer
docker-compose up
```

Now we can use client to connect to the server
```
cd loadBalancer/Client/src/
javac ClientMain.java
java ClientMain
```

Provide localhost as the server IP if containers are also running on the same machine.
If you are remotely connecting to the server then provide the IP of host which is running the server-worker containers.

Input `done` when you want to quit.