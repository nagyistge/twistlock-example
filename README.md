twistlock-example
=================

An example of a container description for the twistlock system.

Requisites
----------

1. A description file
2. Container control script

Description file
----------------
A yaml file with the following properties:

1. A fully qualified name field.
2. A provided services map of service names and the ports at which the services are offered.
3. A consumed services map of service names and the ports at which the services are expected.
4. A resources map of resource names and their expected mount points.

Example:

```
name: blog
provided_services:
    website:
        port: 80
        description: The blog interface served over http.
consumed_services:
    mysql:
        port: 3306
        description: An SQL server for storing entries and comments.
resources:
    logs:
        path: /data/logs
        description: blog application server logs
```

Container control script
-------------------------
There are 4 functions that the script must implement.

1. Build. In this function the container should be prepared. In case of a docker container it could be the invocation of `docker build`.
2. Run. In this function the container should be ran. It should read a series of parameters in over stdin. In the case of docker it would then invoke `docker run` with those parameters. It should return a container identifier.
3. Link. Connect a port of a container to an external service.
4. Stop. Stop a container.
