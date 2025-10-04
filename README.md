
## Setup
To run the cluster, use:

```shell
docker-compose up -d
```

## Test
To connect to cluster nodes:
1. Check what nodes are running (the format is showing a short version of the table):
```shell
docker ps -a --format "table {{.Names}}\t{{.Status}}"
```
Example output:
```terminal
NAMES                                     STATUS
hadoop-cluster-docker_datanode_1          Up 18 minutes
hadoop-cluster-docker_nodemanager_1       Up 18 minutes
hadoop-cluster-docker_resourcemanager_1   Up 18 minutes
hadoop-cluster-docker_namenode_1          Up 18 minutes
```
2. Connect to the node:
```shell
docker exec -it hadoop-cluster-docker_namenode_1  /bin/bash 
```
Example output:
```terminal
bash-4.2$ 
```
^ that means, you'r at cluster. Validate it:
```shell
bash-4.2$ hostname
namenode 

# check pre-installed examples at cluster:
bash-4.2$ ls share/hadoop/mapreduce/
hadoop-mapreduce-client-app-3.3.6.jar	  hadoop-mapreduce-client-hs-plugins-3.3.6.jar	     hadoop-mapreduce-client-shuffle-3.3.6.jar	 lib-examples
hadoop-mapreduce-client-common-3.3.6.jar  hadoop-mapreduce-client-jobclient-3.3.6-tests.jar  hadoop-mapreduce-client-uploader-3.3.6.jar  sources
hadoop-mapreduce-client-core-3.3.6.jar	  hadoop-mapreduce-client-jobclient-3.3.6.jar	     hadoop-mapreduce-examples-3.3.6.jar
hadoop-mapreduce-client-hs-3.3.6.jar	  hadoop-mapreduce-client-nativetask-3.3.6.jar	     jdiff
```
Run some example with `yarn`
```shell
bash-4.2$ yarn jar  share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.6.jar 
An example program must be given as the first argument.
Valid program names are:
  aggregatewordcount: An Aggregate based map/reduce program that counts the words in the input files.
  aggregatewordhist: An Aggregate based map/reduce program that computes the histogram of the words in the input files.
  bbp: A map/reduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.
  dbcount: An example job that count the pageview counts from a database.
  distbbp: A map/reduce program that uses a BBP-type formula to compute exact bits of Pi.
  grep: A map/reduce program that counts the matches of a regex in the input.
  join: A job that effects a join over sorted, equally partitioned datasets
  multifilewc: A job that counts words from several files.
  pentomino: A map/reduce tile laying program to find solutions to pentomino problems.
  pi: A map/reduce program that estimates Pi using a quasi-Monte Carlo method.
  randomtextwriter: A map/reduce program that writes 10GB of random textual data per node.
  randomwriter: A map/reduce program that writes 10GB of random data per node.
  secondarysort: An example defining a secondary sort to the reduce.
  sort: A map/reduce program that sorts the data written by the random writer.
  sudoku: A sudoku solver.
  teragen: Generate data for the terasort
  terasort: Run the terasort
  teravalidate: Checking results of terasort
  wordcount: A map/reduce program that counts the words in the input files.
  wordmean: A map/reduce program that counts the average length of the words in the input files.
  wordmedian: A map/reduce program that counts the median length of the words in the input files.
  wordstandarddeviation: A map/reduce program that counts the standard deviation of the length of the words in the input files.
```

## Teardown
To shutdown:
Run from your Host OS terminal, not from namenode in Hadoop cluster!! :)
```shell
docker-compose down
```
