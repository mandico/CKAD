https://betterprogramming.pub/understanding-kubernetes-multi-container-pod-patterns-577f74690aee

###Sidecar
Sidecars derive their name from motorcycle sidecars. While your motorcycle can work fine without the sidecar, having one enhances or extends the functionality of your bike, by giving it an extra seat. Similarly, in Kubernetes, a sidecar pattern is used to enhance or extend the existing functionality of the container.
Your container works perfectly well without the sidecar, but with it, it can perform some extra functions. Some great examples are using a sidecar for monitoring and logging and adding an agent for these purposes.
![Sidecar](https://miro.medium.com/max/722/1*oeSs9sh6YF1MS23yOu_SEQ.png)

###Ambassador
The ambassador pattern derives its name from an Ambassador, who is an envoy and a person a country chooses to represent their country and connect with the rest of the world. Similarly, in the Kubernetes perspective, an Ambassador pattern implements a proxy to the external world. Let me give you an example — If you build an application that needs to connect with a database server, the server configuration, etc, changes with the environment.
Now, the official recommendation to handle these is to use Config Maps, but what if you have legacy code that is already using another way of connecting to the database. Maybe, a properties file, or even worse, a hardcoded set of values. What if you want to communicate with localhost, and you can leave the rest to the admin? You can use the Ambassador pattern for these kinds of scenarios.
So, what we can do is create another container that can act as a TCP Proxy to the database, and you can connect to the proxy via localhost. The sysadmin can then use config maps and secrets with the proxy container to inject the correct connection and auth information.
![Ambassador](https://miro.medium.com/max/702/1*KezIya2fucCvNSx99CI23A.png)

###Adapter
The Adapter is another pattern that you can implement with multiple containers. The adapter pattern helps you standardise something heterogeneous in nature. For example, you’re running multiple applications within separate containers, but every application has a different way of outputting log files.
Now, you have a centralised logging system that accepts logs in a particular format only. What can you do in such a situation? Well, you can either change the source code of each application to output a standard log format or use an adapter to standardise the logs before sending it to your central server. That’s where the adapter pattern comes in.

![Adapter](https://miro.medium.com/max/482/1*eQ2gXcum3e7ADOdBrjKS5A.png)