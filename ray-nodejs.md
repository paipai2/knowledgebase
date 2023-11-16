# Technical Articles
<p align="center">
  <a href="https://github.com/madxradicle/madxframework2.0">
    <img src="https://github.madxradicle.com/MR_logo.png" alt="Logo" width="200px" height="100px">
  </a>
  <h3 align="center">Technical Articles</h3>
  <p align="center">
   These articles are initially written in chinese and they're moved from google documents.
    <br />
    <a href="https://github.com/madxradicle/articles"><strong>Explore the docs »</strong></a>
    <br />
    <a href="https://github.com/madxradicle/articles/issues">Report Bug</a>
    ·
    <a href="https://github.com/madxradicle/articles/issues">Request Feature</a>
  </p>
</p>

#use putty to access
```
```
#Go to directory, root directory will display charity and ray folder

```
cd ~
```
# use ls display the folder
```
ls
```
# example go to fray folder

```
cd ray
```

# BUILD: the application for change any setting
```
yarn build
```

#START: the program with 8081 port

```
PORT=8081 yarn start
```

---------------------------------------------------------------------------------------
# so at website just type and see result with 8082 port
```
http://34.87.68.208:8081
```


# troubleshooting if any error✅

PORT=8082 yarn start face any error of screen, like 8082 port already on there, use below check the port
[root@instance-4-fatt3 charity]# PORT=8081 yarn start

# Below of this the ports have being use, show a error like below 8081 was use
```
yarn run v1.22.19
$ next start
 ⨯ Failed to start server
Error: listen EADDRINUSE: address already in use :::8081
    at Server.setupListenHandle [as _listen2] (node:net:1463:16)
    at listenInCluster (node:net:1511:12)
    at Server.listen (node:net:1599:7)
    at /home/charity/node_modules/next/dist/server/lib/start-server.js:254:16
    at new Promise (<anonymous>)
    at startServer (/home/charity/node_modules/next/dist/server/lib/start-server.js:191:11)
    at nextStart (/home/charity/node_modules/next/dist/cli/next-start.js:50:40)
    at /home/charity/node_modules/next/dist/bin/next:157:54
    at async main (/home/charity/node_modules/next/dist/bin/next:157:5) {
  code: 'EADDRINUSE',
  errno: -98,
  syscall: 'listen',
  address: '::',
  port: 8081
}
error Command failed with exit code 1.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.

```


```
netstat -tuln
```
<h2>should have the port use at there, you can see at there✅</h2>

[root@instance-4-fatt3 charity]# netstat -tuln
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:443             0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.1:43300         0.0.0.0:*               LISTEN     
tcp6       0      0 :::8082                 :::*                    LISTEN     
tcp6       0      0 :::22                   :::*                    LISTEN     
tcp6       0      0 ::1:25                  :::*                    LISTEN     
udp        0      0 0.0.0.0:68              0.0.0.0:*                          
udp        0      0 127.0.0.1:323           0.0.0.0:*                          
udp6       0      0 ::1:323                 :::*                               
udp6       0      0 :::57997                :::*                               
udp6       0      0 :::45937                :::*                               
udp6       0      0 :::60195                :::*                               
udp6       0      0 :::56952                :::*        


<h2>Then should use ps aux | grep yarn✅</h2>
```
ps aux | grep yarn
```

# can see the below yarn already running ✅
[root@instance-4-fatt3 charity]# ps aux | grep yarn
root     31922  0.0  0.5 918616 47216 pts/0    Sl+  12:10   0:00 node /usr/bin/yarn start
root     32171  0.0  0.0 112808   968 pts/1    D+   12:40   0:00 grep --color=auto yarn

# so just kill it the 31922 in the list ✅

```
kill -9 31922
```

# so now you can run port 8080 smoothly no any error ✅
```
PORT=8081 yarn start
```



# Beware to use below of command:❗
# REMOVE DIRECTORY (USE WITH CAUTION):❗
rm -rf directory_name 

# RENAME DIRECTORY: ❗
mv ori_name renamed

# COPY DIRECTORY:📋 
cp -r ori_directory new_directory

ADD NEW PAGE (NEXTJS):

Header: src/components/elements/navigation/NavBar/paths.ts
Controller: src/components/templates/NEWDIRECTORY
Pages: pages/NEWPAGE
