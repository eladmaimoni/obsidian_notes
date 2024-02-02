
### Generating Private / Public Keys
Generate public / private key pairs, putting them by default on `~/.ssh/id_rsa` which is the User folder on windows / linux

```
ssh-keygen -t rsa 
cat ~/.ssh/id_rsa.pub # will print public key to the console
```

### Setting Password Bypass

```
# connecting 
ssh username@ip-address

# copy the key to another machine such to allow connecting without password
# note that an extra step is needed - adding the IdentityFile to `~/.ssh/config` 
ssh-copy-id -i ~/.ssh/id_rsa.pub dev@192.168.252.86
```

## SSH Configuration file
your machine has a configuration file (`~/.ssh/config`) where it lists some known remote machines with their IP address and user.

- example:
```
Host linux-nuc
     HostName 192.168.252.86
     User dev   
     IdentityFile ~/.ssh/id_rsa
```
- Note the IdentityFile. this lets you automatically connect\
