[root@server-1 ~]# docker system prune -a
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all images without at least one container associated to them
  - all build cache

Are you sure you want to continue? [y/N] y
Deleted Containers:
1107c25085f8ee942c54013bba10e50ffa76911a8ae95954c931a82aa7867cda

Deleted Networks:
csvserver_default
solution_default
solutions_default
root_default

Deleted Images:
untagged: infracloudio/csvserver:latest
untagged: infracloudio/csvserver@sha256:20bc5a93fac217270fe5c88d639d82c6ecb18fc908283e046d9a3917a840ec1f
deleted: sha256:8cb989ef80b5708fc30467273a62e340f620838ac9e9b2e33a54160e2aad7271
deleted: sha256:cc9ea2c5f052a30cc51eb3ab863d8f4034e822ff6f02d10669d0635ce8beb3ab
deleted: sha256:e11d389f63c902f826e1ec375b9a15df04c973523925e69c2a28e5dd036ff3fe
deleted: sha256:4d330ab6e8a980ae73947d118271068b3ebc6cdc23571fcecf469243fdbd00e0

Total reclaimed space: 237.2MB
[root@server-1 ~]# client_loop: send disconnect: Connection reset


[root@server-1 solution]# docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@server-1 solution]# docker container ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@server-1 solution]#

[root@server-1 prometheus]# docker image ls
REPOSITORY        TAG       IMAGE ID       CREATED         SIZE
prom/prometheus   v2.22.0   7adf5a25557b   16 months ago   168MB
[root@server-1 prometheus]#


[root@server-1 ~]# docker-compose up -d
Recreating root_prometheus_1 ... done
[root@server-1 ~]# docker container ps
CONTAINER ID   IMAGE                     COMMAND                  CREATED         STATUS         PORTS                                       NAMES
54aff21bf2dc   prom/prometheus:v2.22.0   "/bin/prometheus --w…"   6 seconds ago   Up 5 seconds   0.0.0.0:9000->9090/tcp, :::9000->9090/tcp   root_prometheus_1
[root@server-1 ~]# docker container ps -a
CONTAINER ID   IMAGE                     COMMAND                  CREATED              STATUS              PORTS                                       NAMES
54aff21bf2dc   prom/prometheus:v2.22.0   "/bin/prometheus --w…"   About a minute ago   Up About a minute   0.0.0.0:9000->9090/tcp, :::9000->9090/tcp   root_prometheus_1



