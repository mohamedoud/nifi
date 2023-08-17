# Build Environment

The Docker image in `Dockerfile` is based on the TDP build image.

The image can be built and the container should be started by running this script: `./bin/start-build-env.sh`

## Building
Run the following Maven command to build standard project modules of nifi:

```
mvn clean install -DskipTests 
```

Change directories to `nifi-assembly/target`. The target directory contains binary archives.

drwxr-xr-x  3 builder  builder   102B Apr 30 00:29 target/nifi-1.23.0-bin
-rw-r--r--  1 builder  builder   144M Apr 30 00:30 target/nifi-1.23.0-bin.tar.gz
-rw-r--r--  1 builder  builder   144M Apr 30 00:30 target/nifi-1.23.0-bin.zip

## Skipped tests

java.lang.NullPointerException
	at org.apache.nifi.processors.standard.TestExecuteProcess.validateProcessInterruptOnStop(TestExecuteProcess.java:123)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at java.util.ArrayList.forEach(ArrayList.java:1259)
	at java.util.ArrayList.forEach(ArrayList.java:1259)


## Build docker image:
After running a full NiFi build, you can generate a Docker image based on the build by executing the following command:

```
mvn install -Pdocker -pl nifi-docker/dockermaven
```

After it completes successfully, you should have an apache/nifi:1.23.0-maven image.


To build all nifi dockermaven images :

```
mvn install -Pdocker -pl nifi-toolkit/nifi-toolkit-assembly,nifi-docker/dockermaven,nifi-registry/nifi-registry-docker-maven/dockermaven,minifi/minifi-docker,minifi/minifi-c2/minifi-c2-docker
```
