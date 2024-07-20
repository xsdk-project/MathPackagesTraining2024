---
layout: page
show_meta: false
title: "Setup Instructions"
header:
   image_fullwidth: "atpesc-1024x2746.jpg"
permalink: "/setup_instructions/"
---

All handson activity will be on [Polaris](https://docs.alcf.anl.gov/polaris/getting-started/). Here are instructions that are common
for all the lessons.

## Using Polaris

1. Log into Polaris
```
ssh -l <username> -Y polaris.alcf.anl.gov
```
1. Copy Installed Software
* Once you are logged into Polaris, please execute the following instruction
to create a local, editable copy of numerical package software.
```
cd ~
rsync -a {{site.handson_install_root}}/{{site.handson_root}} .
```
  * **Note 1:** do not include a trailing slash, `/` in the path argument.
  * **Note 2:** You may be asked periodically throughout the day to re-execute
this command to update your local copy if we discover changes are necessary.
1. Schedule a Polaris compute node for compiles and runs
```
qsub -I -l select=1 -l filesystems=home:eagle -l walltime=1:00:00 -q debug -A ATPESC2024
```
  * **Note 2:** One *cannot* (compile or) run the binaries on the frontends. Use the allocated node for such usage.
  * **Note 3:** Polaris job scheduling policies [document](https://docs.alcf.anl.gov/polaris/running-jobs/)
  * **Note 4:** To enable X windows for visualization on the compute node, you can open a new terminal and login to the allocated compute node by doing `ssh -Y polarisXY` (`polarisXY` is your compute node id)
1. Load the required modules
```
module swap PrgEnv-nvhpc PrgEnv-gnu
module load nvhpc-mixed craype-accel-nvidia80
module use /soft/modulefiles
module load spack-pe-base
module load cmake ninja
module load cray-libsci
```

#### Miscellaneous ssh instructions

Usig ssh `control master` feature helps with repeated access to `polaris`. For this, one can add (say on your laptop) the following to `~/.ssh/config`
```
Host polaris.alcf.anl.gov
    Compression yes
    ForwardX11 yes
    ForwardX11Trusted yes
    ControlMaster auto
    ControlPersist 12h
    ControlPath ~/.ssh/%r@polaris.alcf.anl.gov:%p
```
With this setup - the first time you login polaris.alcf.anl.gov - you need to provide passwd. But subsequent ssh/scp/sftp will go through this control master - and not ask for passwd

Beyond that, you may also want to have a look at...

* [Setting Up & Using SSH Multiplexing / Control master](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Multiplexing)
* [Using SFTP](https://www.digitalocean.com/community/tutorials/how-to-use-sftp-to-securely-transfer-files-with-a-remote-server)
* [Mounting Filesystems Over SSHFS](https://wiki.archlinux.org/index.php/SSHFS)

