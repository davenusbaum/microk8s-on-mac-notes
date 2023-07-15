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

