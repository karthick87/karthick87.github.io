---
layout: post
title:  "Docker Basics"
date:   2022-07-28 15:00:00 +0900
categories: update
---

# Executing commands directly on the Container

```shell
docker exec -it <container> bash -c 'rm -rf /tmp/.*'
```

# Running Jupyter Notebooks in a Container

```shell
docker volume create jupyter-notebooks 
docker run  -p 8888:8888 --name notebooks -e JUPYTER_ENABLE_LAB=yes --volume=jupyter-notebooks:/home/jovyan/work jupyter/datascience-notebook
```

Note: Only Notebooks saved inside work directory will be persistent. 

# Destructive Command

```shell
docker system prune --all --volumes --force
docker builder prune
docker builder prune --all
```

# Mapping of overlay2 Folders to exact RepoDigest information
```shell
$ docker image inspect $(docker image ls -q)  --format '{{ .GraphDriver.Data.MergedDir}} -> {{.RepoDigests}}' | sed 's|/merged||g'
```

# To Remove all Log Files
```shell
$ find /var/lib/docker/containers/ -type f -name “*.log” -delete
```
