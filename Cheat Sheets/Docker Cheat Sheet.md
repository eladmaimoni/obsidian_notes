
# Cleanup Commands
### Remove All Stopped Containers

```
docker container prune
```
## Global Configuration

### Setting an alternative location for docker persistent data:

https://stackoverflow.com/questions/55344896/attempt-to-change-docker-data-root-fails-why

```
sudo systemctl stop docker
sudo rsync -axPS /var/lib/docker/ /mnt/x/y/docker_data # copy all existing data to new location
sudo nano /lib/systemd/system/docker.service # or your favorite text editor
```

edit the file /etc/docker/daemon.json
(exiting nano is via CTRL+x , y and then hitting ENTER)

```bash
sudo systemctl daemon-reload
sudo systemctl start docker
docker info | grep "Root Dir"
```


Alternative method: (Didn't work for me)
```
sudo systemctl stop docker
sudo nano /etc/docker/daemon.json

{
    "runtimes": {
     "data-root": "/media/nvidia/docker_data",
     "nvidia": {
            "args": [],
            "path": "nvidia-container-runtime"
        }
    }
}
sudo systemctl restart docker
sudo systemctl status docker
```



