# Environment
### Reload bashrc
```
source ~/.bashrc
```
### Switching password: `passwd`

# Filesystem
### Finding file system wide
```
sudo find / -name "*string-inside*"
```
### Copying files to remote machine
```
sudo find / -name "*string-inside*"
```
### Display directories by size
```
sudo du -sh ./* | sort -h
sudo du -sh /var/lib/* | sort -h
```
# APT Package Manager
### Listing All Installed Packages by Size 
```
dpkg-query -Wf '${Installed-Size}\t${Package}\n' | sort -n
``