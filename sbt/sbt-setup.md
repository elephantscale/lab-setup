<link rel='stylesheet' href='../assets/css/main.css'/>

Install SBT
=====================

### Overview
Install and run Zookeeper

### Depends On
None

### Run time
10 mins


## Step 1 : Install sbt
Try this in terminal
```bash
    $ echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
    $ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
    $ sudo apt-get update
    $ sudo apt-get install sbt
```

