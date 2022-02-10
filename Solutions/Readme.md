git clone https://github.com/infracloudio/csvserver
git checkout -b sandeep

docker pull infracloudio/csvserver:latest
docker pull prom/prometheus:v2.22.0


docker images ls 
output:
[root@server-1 ~]# docker image ls
REPOSITORY               TAG       IMAGE ID       CREATED         SIZE
infracloudio/csvserver   latest    8cb989ef80b5   11 months ago   237MB
prom/prometheus          v2.22.0   7adf5a25557b   16 months ago   168MB
[root@server-1 ~]#

[root@server-1 ~]# docker run -d infracloudio/csvserver:latest
21109b803b263ab33f6a347ef00663eccc77fe9c1bc0fa918494558afcb6d9e4
[root@server-1 ~]# docker logs 21109
2022/02/09 14:42:06 error while reading the file "/csvserver/inputdata": open /csvserver/inputdata: no such file or directory
[root@server-1 ~]#

Part 1

[root@server-1 solution]# cat gencsv.sh
#/bin/bash
# enter the number of random numbers required
read -p  "Enter the number of random numbers: " rnumber

for i in $(seq $rnumber) ; do echo $i, $(shuf -i 1-$rnumber -n 1)  ; done > inputFile

[root@server-1 solution]# ./gencsv.sh
Enter the number of random numbers: 20
[root@server-1 solution]#

[root@server-1 solution]# cat inputFile
1, 19
2, 6
3, 18
4, 8
5, 15
6, 16
7, 1
8, 17
9, 5
10, 4
11, 16
12, 19
13, 5
14, 10
15, 19
16, 2
17, 15
18, 7
19, 4
20, 5
[root@server-1 solution]#


[root@server-1 solution]# docker run -d -p 9393:9300  --mount type=bind,source="$(pwd)"/inputFile,target=/csvserver/inputdata  infracloudio/csvserver
6ba3304764f7b3367ef03298f8a7b974512de165576577f6d01382d955f2c54c
[root@server-1 solution]# docker ps
CONTAINER ID   IMAGE                    COMMAND                  CREATED         STATUS         PORTS                                       NAMES
6ba3304764f7   infracloudio/csvserver   "/csvserver/csvserver"   4 seconds ago   Up 3 seconds   0.0.0.0:9393->9300/tcp, :::9393->9300/tcp   relaxed_leavitt
[root@server-1 solution]# ls
gencsv.sh  inputFile
[root@server-1 solution]#




