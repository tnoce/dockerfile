# Toolbox docker image and container

## Prepare docker image and container run

### Docker image

```
docker build -t arimas/toolbox:<tag> .
```

### Container run and mount volume

```
docker run -itd --name <Container name> -v <Local git directory>:/root/work <Docker image name> /bin/bash
```
