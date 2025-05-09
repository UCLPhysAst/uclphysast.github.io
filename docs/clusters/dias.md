# DIAS

## Overview

The DIAS cluster offers access to a small number of powerful CPU and GPU systems. It is available to researchers in Physics and Astronomy who need more powerful resources than their own desktop or laptop computers, but don't need low-latency networking for multi-node parallel computation (for which the [Hypatia](hypatia.md) cluster may be more suitable) or the larger clusters provided by [ARC](https://www.rc.ucl.ac.uk/docs/) or national facilities. It is available to masters (MSc and MSci) students undertaking research projects, where requested by the student's supervisor.

## Account creation and support

To request an account on DIAS, please e-mail [phy.dias.support@ucl.ac.uk](mailto:phy.dias.support@ucl.ac.uk) with the following information:

- your name;
- your UCL computing ID (e.g. ucapxxx);
- your research group affiliation (Astro, AMOPP, BioP, CMMP, HEP).

UCL email addresses (i.e. of style <first_name>.<surname>.<year>@ucl.ac.uk) are mandatory, as no account information will be sent to non-UCL email addresses.

For masters students, the request must be made by the project supervisor or course leader, and should also include:

- supervisor's name;
- supervisor's UCL computing ID (e.g. ucapxxx);
- supervisor's UCL e-mail address.

Masters students should also contact their supervisor in the first instance with any queries or problems relating to the DIAS cluster. The supervisor can decide if a problem requires system administrator support.

## Access

Access to DIAS is by SSH to dias.hpc.phys.ucl.ac.uk, e.g. `ssh username@dias.hpc.phys.ucl.ac.uk`. DIAS access requires that you be within the UCL network. 

If you are not on site at UCL you can still access the cluster by using 

- [the UCL VPN](https://www.ucl.ac.uk/isd/services/get-connected/ucl-virtual-private-network-vpn));
- [Desktop@UCL Anywhere](https://www.ucl.ac.uk/isd/services/computers/remote-access/desktopucl-anywhere);
- [the SSH gateway](https://www.rc.ucl.ac.uk/docs/Remote_Access/).

If you encounter any issue or need assistance with these services you will need to contact the [ISD Service Desk](https://www.ucl.ac.uk/isd/help-support).

For running graphical applications remotely from a Windows machine you will need an X server application. We recommend you install OpenSSH on your Windows machine. This is the easiest solution to connecting to SSH via windows as it is also a native application on Unix systems.

Alternatively you can find programs such as Exceed, which can be downloaded from the UCL software database: http://swdb.ucl.ac.uk/package/view/id/150 and an SSH client that supports X11 forwarding (e.g. PuTTY: https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

This video tutorial may be useful for Desktop@UCL users: [Connecting to a Linux system from Desktop@UCL](https://www.youtube.com/watch?v=v_Gz8oZcsXQ).

## Using the cluster


The DIAS cluster runs a variant of the CentOS 7 Linux operating system. Using Linux remotely you will mainly use a terminal interface running ‘bash’.

If you are new to Linux or Research computing you can find some helpful online courses and resources provided by UCL ARC in the [ARC Course Catalogue](https://www.ucl.ac.uk/advanced-research-computing/training/course-catalogue).

If you are looking for a more casual approach to learning how to use a Linux system you can find many websites with useful commands, examples and tutorials.

Please note that data on DIAS is not backed up and you should keep code in external source control and otherwise keep copies of data elsewhere.

DIAS operates in the style of an HPC cluster. HPC clusters differ somewhat in how they are used from conventional computing, in that the sorts of large or processor intensive jobs used on them must be submitted to a job manager so that appropriate resources are allocated and do not conflict with other jobs.

The node you log in to is the login node. In the case of Dias this is also the head node which manages the cluster. It's important for other users and the cluster as a whole that high memory or processor intensive jobs are never run on this node. If such jobs are found to be running they will be terminated without warning. You are encouraged to run normal editing and development work on the login node however, so you can edit files, download data, check your work into repositories, move files around and so on without a problem.

When you come to run intensive jobs, you must request a job from the job manager, which in the case of Dias is software called Slurm (Simple Linux Utility for Resource Management). This software will allocate your job to one of the two CPU nodes, or the GPU node. If Dias is busy there may be a wait for resources, but Slurm tries to allocate resources fairly so that users get an appropriate share of the time.

Resources are divided into partitions which contain different types of hardware - for Dias these are normal CPU nodes in the COMPUTE partition, one GPU node in the GPU partition, and one GPU node in the LIGHTGPU partition.

### Submitting a job to Slurm
To submit a job you must write a bash script that has the commands needed to run your code, and also includes directives to Slurm for what resources are needed. This script is then submitted using the sbatch command. The directives to Slurm are special comment lines beginning with *#SBATCH*. 

In the example below these are interleaved with normal explanatory comments. This can be difficult to understand, so don't hesitate to ask for help if needed.

An example job script might look like
```
#!/bin/bash
#submit to the normal COMPUTE partition for normal CPUS
#SBATCH -p COMPUTE
#request a different amount of time to the default 12h
#SBATCH --time 24:00:00
#requesting one node
#SBATCH -N1
#requesting 12 cpus
#SBATCH -n12
#SBATCH --mail-user=youremail@ucl.ac.uk
#SBATCH --mail-type=ALL
cd /home/username/programlocation
srun ./program 
```

The job is submitted with 'sbatch scriptname' and you will be given a job number by Slurm. The *srun* command is a special part of Slurm that unlocks multiple processors for MPI code. There are different technologies for different kinds of multiple processor use, so if your code uses multiple processors you may want to contact technical support to make sure you are doing so correctly. Your supervisor may be able to advise on whether the code is for example OpenMP, MPI, or uses some other method, and providing this information to us will help us get your code running well.

### GPU requests
A request for a GPU node must also request one or more of its NVIDIA A100 cards. This is done with something like
```
#!/bin/bash
#SBATCH -p GPU
#SBATCH --gres=gpu:a100:1
```
The 1 at the end of the line requests 1 card. More can be requested but these are valuable resources and you should be sure your code makes good use of multiple cards and will not run for too long blocking out other users. Resources for CPUs can be requested still with the -n option. The GPU partition has 3 40GB A100 cards available. The LIGHTGPU partition (selected by using *#SBATCH -p LIGHTGPU* ) has the same hardware but divided into 6 20GB instances. If you can use the LIGHTGPU partition instead, please do, but note that you must only request one GPU per job in this partition.

LIGHTGPU users may need to switch the first line of their script to
```
#!/bin/bash -l
```
in order to correctly have the CUDA_VISIBLE_DEVICES variable set, or alternatively add
```
source /etc/slurm/gpu_variables.sh
```
to your job script at the start.

### Interactive jobs
A simple interactive job can be run by using srun in a different mode to call a shell. srun will make the necessary resource request, and you do not need to use the sbatch command in this case.
```
srun --spankx11 --pty bash
```
Further arguments can be used to request additional resources beyond just one processor, e.g. '*srun -N1 -n2 --pty bash*' for two processors on one node.

### Other resources
As well as how many CPUs or GPUs to request you may need to request a certain amount of memory, otherwise you will be limited to 2GB per CPU requested. It is important to be accurate with how much memory you need, but it is more important to overestimate the amount. If you ask for too much the worst that will happen is that other users may have to wait a bit longer for code to run, but if you ask for too little your program will fail, and you will have to resubmit your job and other users will may have to wait for your code to rerun anyway! These resources are requested with a line like this for a request per CPU requested:
```
#SBATCH --mem-per-cpu 4G
```
or just for the total amount
```
#SBATCH --mem 4G
```
You are also encouraged to specify how long your job might take - like the memory request this should always overestimate so that your job will not be killed. You can request a maximum of two days runtime, and if you specify no time you will be allocated a default of 12 hours after which your job will be ended, but if you specify a time otherwise it helps Slurm slot your job in to its queue during busy periods. You can do this with a request like
```
#SBATCH --time 12:00:00
```

## Python
You may wish to use [Miniforge](https://github.com/conda-forge/miniforge) to create Python environments. 

### Jupyter
You can use Jupyter notebooks using a version of the script found at /share/apps/anaconda/jupyter-slurm.sh. You should make a copy, take a look through it, and alter parameters at the start as needed for a Slurm script, e.g. changing the partition to use a GPU. Also note the activation of Anaconda towards the end - you may want to activate your own environment here.
The script will start Jupyter on one of the nodes, and give you connection instructions to connect your local machine to it (open the jupyter-notebook-xxx.log file created). These assume the use of Linux or Mac style command line ssh. If you are using PuTTY for example, you will need to use the port numbers and the node name in the port forwarding configuration of PuTTY.

For example, at the top of your log file you will see a line like
To connect:
```
ssh -N -L 8350:compute-0-1:8350 eme@dias.hpc.phys.ucl.ac.uk
```
If using PuTTY you need to connect to dias, port forwarding to host compute-0-1 with local and remote ports both 8350.

**Important: You should use *scancel* to end the Jupyter job when you are done with the session, or it will continue to run and block resources.**
 
The job number can be found in the output of squeue, and it is also the number in the appropriate jupyter-notebook-xxx.log filename.