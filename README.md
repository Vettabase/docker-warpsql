# vettadock/warpsql Docker image

Dockerfiles to build Docker images for WarpSQL.

WarpSQL is a MySQL fork by Justin Swanhart. Its main feature is the WARP engine, that
can be used for analytics or to move starships.

Maturity level of the Dockerfiles: alpha.


## Building the image

To build the image from a Dockerfile, first move to the Dockerfile directory, then run:

```
docker build --no-cache --tag vettadock/warpsql:8.0-1.0 .

```


## Create and use a container

A container can be used in this way:

```
docker run --detach --name <container-name> vettadock/warpsql:8.0-1.0
docker start <container-name>
```

To connect WarpSQL using the mysql client inside the container:

```
docker exec -ti <container-name> mysql
```


## Security concerns

When a container is created, the root user has no password. At this point there is not data,
so creating a temporary password would bring no benefit. Creating proper users and
passwords is your responsibility.

We believe that official MySQL, Percona Server and MariaDB containers should do the same by
default, even if it sounds less cool.

WarpSQL runs as mysql:mysql. Any other command run via do `docker exec` will run as root.
However, to run such commands you need to be root in the host. This allows you to access
all containers data, destroy containers, and even replace them with a flavour you created.
For this reason, we don't see the root user as a security risk in this context.
However, if you believe there is a valid reason to avoid using root in a container,
please file a bug and explain your point of you. We love to be persuaded when we are wrong.


## TODO

- Add VOLUMEs in Dockerfile
- Add documentation on how to expose ports, specify volumes for containers, or using Docker networks
- Add documentation on how to perform backups


## Credits and contacts

This repository is maintained by Vettabase.

For questions or commercial support inquiries regarding the containerisation of WarpSQL, please
contact info@vettabase.com. Currently we do not offer support for WarpSQL itself.


**If you find this software useful, please consider contributing [WarpSQL](https://warpsql.blog/).**



