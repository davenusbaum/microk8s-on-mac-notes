# MicroK8s on MacOS (Notes)

I want to try Kubernetis for a solution that is distributed across multiple data centers
for continuous availability. [MicroK8s](https://microk8s.io) from Canonical has some features 
that I think make it worth a look for this project. 
My first step is to get an instance running on my Mac so I can do some initial experimentation. 
If that first step works, I'll try a Raspberry Pi based cluster and experiment with network, power 
and disconnected drive failures.

Basic install notes for my M1 based Mac are [here](https://ubuntu.com/tutorials/installing-microk8s-on-apple-m1-silicon#1-installation).

I started with homebrew and ended up with an error:
```
launch failed: instance "microk8s-vm" already exists
```

It's possible I tried MicroK8s in the past, maybe even before moving to an M1 machines,
so it seems I need to clean things up and maybe get a fresh start. These are my notes and references
just in case I end up in the same place again.

```
> multipass info --all
Name:           primary
State:          Running
IPv4:           192.168.64.2
Release:        Ubuntu 22.04.2 LTS
Image hash:     f7555cd22ead (Ubuntu 22.04 LTS)
CPU(s):         1
Load:           0.00 0.00 0.00
Disk usage:     1.6GiB out of 4.8GiB
Memory usage:   137.3MiB out of 962.4MiB
Mounts:         --

Name:           exalted-jaybird
State:          Running
IPv4:           192.168.64.6
Release:        Ubuntu 22.04.2 LTS
Image hash:     f7555cd22ead (Ubuntu 22.04 LTS)
CPU(s):         1
Load:           0.00 0.00 0.00
Disk usage:     1.6GiB out of 4.8GiB
Memory usage:   157.1MiB out of 962.4MiB
Mounts:         --

Name:           microk8s-vm
State:          Unknown
IPv4:           --
Release:        --
Image hash:     f7555cd22ead (Ubuntu 22.04 LTS)
CPU(s):         --
Load:           --
Disk usage:     --
Memory usage:   --
Mounts:         --
```
Suggests there is indeed an instance of microk8s already running.

```
> microk8s enable dashboard
MicroK8s is not running. Please run `microk8s start`.
```

```
> microk8s start
exec failed: Cannot retrieve credentials in unknown state
An error occurred when trying to execute 'sudo microk8s.start' with 'multipass': returned exit code 2.
```

Did some searching and tried
```
> multipass delete microk8s-vm
> multipass purge
> multipass list
Name                    State             IPv4             Image
primary                 Running           192.168.64.2     Ubuntu 22.04 LTS
exalted-jaybird         Running           192.168.64.6     Ubuntu 22.04 LTS
```
So clear everything and start again...
```
multipass delete exalted-jaybird
multipass purge
```
Make sure the packaged version of multipass isn't installed
```
sudo sh "/Library/Application Support/com.canonical.multipass/uninstall.sh"
```
Remove multipass from homebrew
```
brew uninstall --zap multipass
```
