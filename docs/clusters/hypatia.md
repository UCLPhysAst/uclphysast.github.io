# Hypatia

## Overview

The Hypatia cluster supports workloads that are not suitable for [DIAS](dias.md) because they require:

- multiple compute nodes, linked by high-bandwidth, low-latency network connections; or
- GPU nodes.

It consists of two sets of hardware:

- RCIF nodes and storage, which were bought using strategic funds and are open for broad use subject to oversight detailed below;
- Cosmoparticle nodes and storage, which are attached to specific grants and therefore only available by specific users.

## Account creation and support

### RCIF hardware

To ensure the new equipment is used to its best potential, we stated in the bid that access would be limited to those with existing HPC experience. This can be demonstrated through:

- successful completion of a previous project using HPC; or
- completion of a basic level of training provided by UCL or other provider (such as DIRAC). 

In case the facility becomes oversubscribed, a small users’ committee will determine resource allocation, prioritising against the use cases given in the initial RCIF bid.

For new users, training, and early development, other resources are more appropriate. 

In case the facility becomes oversubscribed, a small users’ committee will determine resource allocation, prioritising against the use cases given in the initial RCIF bid. The users’ committee will consist of
- Benjamin Joachimi (chair)
- Edd Edmondson (technical lead)
- Giovanna Tinetti (Group A rep)
- Jim Dobson (HEP rep)
- Sergey Yurchenko (AMOPP rep)

If you would like access please email Edd and Benjamin, stating briefly your HPC experience and intended use for the RCIF facility. Students should arrange for a brief statement of support to also be sent by the supervisor. 

The RCIF segment has 4 nodes with 40 cores and 384GB RAM each. The compute queue for this hardware is 'RCIF', and requires users to be a member of the ‘RCIF’ group (see below for access oversight). RCIF users must remember to submit to the RCIF queue in every batch job - it is not the default.

240TB of hybrid SSD/HDD storage, 1PB of HDD storage, and further compute nodes have been added from RCIF funding. Access to this is separate from other users of Hypatia from the Cosmoparticle Initiative and users must have access approved (and RCIF users will not also automatically get access to the other Hypatia compute and storage facilities). 
Hypatia's GPU facilities (see below) also come under RCIF or CDT access requirements but have a separate partition for use.

### Cosmoparticle hardware

The cosmoparticle hardware is overseen by PIs of the relevant grants which enabled its purchase. Potential users should ask their supervisor/line manager whether they may be able to gain access.

The Cosmoparticle segment has currently has operational 6 nodes with 24 cores each and 256GB RAM, 4 cores with 40 cores each and 320GB RAM, 19 nodes with 64 cores and 512GB RAM, one 'SMP' node with 60 processors and 1.5TB RAM, and one with 80 processors and 1.5TB RAM. The compute queue for this hardware is 'cores64', ‘cores40’, ‘cores24’, ‘smp’, or ‘compute’ to access all non-SMP nodes.

## Storage

There are several additional storage areas for RCIF and Cosmoparticle use beyond the home directories. These areas are not backed up. Additionally, the fastest storage available is individual to each computation node and is that node's local disk. These are usable at /state/partition1 and are about 1TB each, 3TB on the SMP nodes, 2TB on 40 core nodes, and 15TB on GPU nodes. A job that does a lot of reading and writing can use this for the best speed during computations, and you can copy data back and forth from this area to a shared area during your job if needed. When your job has finished, it should tidy up after itself, and data in this area may be deleted without warning when jobs are not running.

The storage areas are as follows - note that at this time /share/data1 is somewhat slower due to being over the login node which is not currently on Infiniband.

| mountpoint | available to | size |
| ---------- | ------------ | ---- |
| /share/hypatia | Cosmoparticle | 64TB |
| /share/data1 | Cosmoparticle | 9TB |
| /share/data2 | Cosmoparticle | 90TB |
| /share/rcifdata | RCIF | 240TB |
| /share/lustre | RCIF | 1PB |

These areas are not backed up (although they have resilience against disk failures). These are a good storage location for data to be seen by all nodes, and which can be recomputed or redownloaded if necessary. When storing data in these areas please do so in a directory named after your username.

Note also that the Lustre area while large can be crippled by having very large numbers of small files in it. Please avoid creating data like this and try to consolidate into smaller numbers of large files.

See the 'Networking and external transfers' section below for how to move data from outside locations to these volumes.

## Access

Login is by SSH to hypatia-login.hpc.phys.ucl.ac.uk.

## Using the cluster

Hypatia runs the Rocks 7.0 Linux distribution and uses Slurm as a job manager. 

The home area has total capacity of about 9TB, which is backed up nightly. Although this has a decent amount of space, please minimise usage of it in order to help with backups and keep space free for new users. Alternative storage areas are described below. The home area is also the slowest tier of storage on Hypatia (although still quite fast).

If you are unfamiliar with HPC environments and using batch submissions to run tasks please contact Edd for advice.

### Job submission
Partition (Queue) names:
- RCIF (RCIF 40 core nodes)
- COMPUTE (all cosmoparticle nodes)
- CORES24 (cosmoparticle 24 core nodes)
- CORES40 (cosmoparticle 40 core nodes)
- CORES64 (cosmoparticle 64 core nodes)
- SMP (cosmoparticle 60+80 core nodes)

Useful links:
- Slurm manual: [https://slurm.schedmd.com](https://slurm.schedmd.com)
- Slurm at COSMA (Durham, DiRAC): [https://www.dur.ac.uk/icc/cosma/support/slurm/](https://www.dur.ac.uk/icc/cosma/support/slurm/)
- Slurm cheatsheet: [https://slurm.schedmd.com/pdfs/summary.pdf](https://slurm.schedmd.com/pdfs/summary.pdf)
- Slurm 'Rosetta Stone' (for converting from the previous PBS/Torque): [https://slurm.schedmd.com/rosetta.pdf](https://slurm.schedmd.com/rosetta.pdf)

### Alerting other users when submitting large numbers of jobs

Most of the time Hypatia runs below full capacity, which is part of its design: we want everyone to be able to access medium-level computing resources flexibly and at short notice.

Please alert other users if you are queueing a large number of simultaneous runs, i.e. that is likely to use >~50% of a given node type at a time.

You can do this by sending an email to the hypatia-users mailing list, so that people can either plan around your usage or — if they have an urgent need for resource — they can request that you throttle back. (You should be subscribed to this list on creation, and a link to the mailing list page is given on login)

## GPUs
Hypatia has six very powerful GPU nodes available to RCIF users and CDT users.

The first four nodes have 384GB RAM, 15TB of very fast NVMe SSD storage, and 24 Intel Xeon Silver 4214 cores. Two of these nodes have 10 V100 GPUs, each capable of 7 Tflops double precision, 14 Tflops single precision, and 112 Tflops half precision, with 16 GB RAM on the GPU. Two further nodes have 5 and 4 A100 GPUs each capable of 9.7 Tflops double precision, 19.5 Tflops single precision, and 312 Tflops half precision, and either 40 GB or 80 GB memory (4x 80 GB, and 4x 40 GB plus 1 80 GB).

A fifth node has 4 80 GB A100 GPUs connected by NVLink, which much upgrades the communication between the GPUs and particularly suits multiple GPU work. It has 512GB RAM and 32 Xeon Silver 4314 cores.

The sixth node has 64 AMD EPYC cores, 1.5TB memory, and 10 L40S cards. The L40S cards each have 48GB on board memory, and for many tasks are comparable in speed to an A100 card but have poor double precision performance.

The A100 cards are very popular due to their higher speed, memory capacity and improved feature set. As a result of their popularity queue times to get on to A100 cards can be quite long. However, the V100 cards are still very capable, and are sufficient for many tasks. Use of the V100 cards is encourage to alleviate pressure on the A100 cards, so if your job doesn’t require the memory or features of the A100 please consider using V100s instead. The slight increase in job times will often be compensated by reduced queuing and this makes the cluster more efficient for everyone. The L40S cards as stated above are also excellent for many tasks, but will be very slow for double precision calculations so it's best to do small test runs on these cards first to see if they suit your code.

Further Grace Hopper systems are due to be installed soon, which will expand these options further.

The GPU nodes have CUDA installed natively, and Apptainer (formerly Singularity) is available if you need to run a containerised OS (contact Edd if you'd like more info on this). The nodes are accessed by the GPU partition. The GPUs are requested through Slurm Generic Resource (GRES) requests. The CUDA_VISIBLE_DEVICES will be suitably set to restrict you to the GPUs allocated. To specify a type of GPU you can either do this in the gres field, e.g.
```
#SBATCH --gres=gpu:a100:1
```
or in the constraints field (which allows multiple types) e.g.
```
#SBATCH --gres=gpu:1
#SBATCH --constraint='a100|l40s'
```
The very fast NVMe storage is available per node in /state/partition1, with 15TB per node (see Storage, above). This is a comparatively small but extremely fast scratch area - please only keep data on it while working on data on a node and remove it to larger volumes afterwards. It’s acceptable to keep data in the area between jobs if it will only be up to a few days between submissions, but old data may be cleared out if left untouched (we will try to contact you first).

For information on running containers (e.g. to use Tensorflow on the GPUs) please see [Containers and Tensorflow-GPU usage on clusters](https://liveuclac.sharepoint.com/sites/PhysAstAstPhysGrp/SitePages/PhysAstAstPhysGrp-Containers-and-Tensorflow-GPU-usage-on-clusters-125937485.aspx).

### Example job
```
#!/bin/bash
#SBATCH -p GPU
#requesting one node
#SBATCH -N1
#requesting 12 cpus
#SBATCH -n12
#requesting 1 V100 GPU
#SBATCH --gres=gpu:v100:1
#SBATCH --mail-user=e.edmondson@ucl.ac.uk
#SBATCH --mail-type=ALL
echo $CUDA_VISIBLE_DEVICES
./program 
```

## VSCode Usage

Visual Studio Code (VSCode) can cause problems on shared systems due to both high load and its tendency to search networked filesystems without prompting, clogging up the network on the login node. VSCode processes may be killed without warning, and the system is set to prioritise these for killing if memory resources become overloaded. Please take the time to set the **files.watcherexclude**, **search.exclude**, and **search.include** parameters to exclude anything except the specific source code trees you are working on so it does not try to search through large amounts of data over the network. Also please disable **search.followsymlinks**. [This documentation](https://code.visualstudio.com/docs/getstarted/settings) provides details of how to set such parameters as does [this blog post](https://bobbyhadz.com/blog/exclude-folders-from-search-in-vscode#excluding-folders-from-all-searches).

## Software

As well as the system default software, some software is available under the [modules system](http://modules.sourceforge.net) which lets you dynamically alter your environment to use specific versions of software as needed. Edd is happy to add software to this as needed, and otherwise software can be installed in your own user areas located in shared areas (such as /home and /share/hypatia), and then be used across the cluster.
If you wanted to load the boost/1.67.0 package for example, just do 'module load boost/1.67.0' or 'module load boost/1.67.0', and remember to do this in any job submission scripts needing it.

### Python

You may wish to use Miniforge to create Python environments. 

### Jupyter notebooks

Running Jupyter notebooks requires you to unset the environment variable XDG_RUNTIME_DIR. A suggested Slurm script is available here: [jupyter-slurm.sh](https://liveuclac.sharepoint.com/sites/PhysAstAstPhysGrp/SiteAssets/SitePages/PhysAstAstPhysGrp-Hypatia-User-Guide-65201536/jupyter-slurm.sh)

Submit the script with sbatch, modifying SBATCH directives if required, and check the jupyter-notebook-xxx.log files for output containing ssh connection information and notebook tokens (full output can take a minute or two to write out).

### MPI tasks
The currently recommended MPI module is mpi/mvapich/2-2.3.1 but note that the recommended way to run an MPI job with this module in a Slurm job is something like:
```
module load mpi/mvapich/2-2.3.1
srun --mpi=pmi2 ./mpiprogram 
```
OpenMPI is also available. To use it load the module mpi/openmpi/4.0.1.

### OpenMP Jobs
To avoid issues with processor affinity restricting you to running on one core, OpenMP jobs should have the OMP_NUM_THREADS variable set, then be run in the script via 'srun -n1'. Without the srun command, access to the allocated processors will not be granted. For example, do something like
```
#!/bin/bash
#SBATCH -p CORES24
#SBATCH -N1
#SBATCH -n24
cd ~/openmpcode
export OMP_NUM_THREADS=$SLURM_JOB_CPUS_PER_NODE
srun -n1 ./openmp_executable 
```

### Interactive jobs
A simple interactive job can be run by using srun to call a shell. srun will make the necessary resource request. 
```
srun --pty bash
```
Further arguments can be used to request additional resources beyond just one processor; for example, to run an interactive job on CORES40 using 40 processors, run:
```
srun -p CORES40 -N1 -n40 --pty bash
```

For X11 applications, you can add '--x11' as a flag. 

## Networking and external transfers

The default network used is ethernet (1 gigabit/s). This handles standard traffic between the nodes, the home filesystem traffic, and connections to the outside world.

Infiniband is also available providing performance at around 100 gigabit/s. MPI jobs can use Infiniband natively, and there is also IP over Infiniband available by using the .mlnx suffix to node names (e.g. compute-0-4.mlnx).

There are two external interfaces through which all traffic to the outside world must flow. One is a direct connection to the login node, and the other is on the head node which all other nodes make use of. These are 1 gigabit/s. As a result of these bottlenecks, large file transfers are better off using the head node's interface so that interactive use of the login node is not impacted. To do this, it's recommended you log in by ssh to the following nodes to move in or out large amounts of data (small copies are fine over the login node). These nodes allow ssh access without needing a job running on them (unlike compute nodes) but please do not run anything on them except file transfers as they are also responsible for running filesystem exports and we don't want to load them unnecessarily or risk bringing one down by accident.

| data area | transfer node |
| --------- | ------------- |
| /share/hypatia | nas-0-0 |
| /share/data1 | login node |
| /share/data2 | nas-0-0 |
| /share/rcifdata | nas-0-1 |
| /share/data3 | nas-0-2 |

As Hypatia is firewalled from the outside world, to do a large transfer via zuserver1 or another UCL gateway machine use a command similar to this:
```
rsync -ave 'ssh -o "ProxyCommand ssh username@zuserver1.star.ucl.ac.uk exec nc %h %p"'filename username@hypatia-login.hpc.phys.ucl.ac.uk:/location/
```

Note that the Lustre area does not have a transfer node. Contact Edd for advice on transferring to this area.

## Acknowledgements in publications
For RCIF hardware we recommend adding the following acknowledgement to publications:

> This work used computing equipment funded by the Research Capital Investment Fund (RCIF) provided by UKRI, and partially funded by the UCL Cosmoparticle Initiative.

For work using Cosmoparticle facilities:

> This work used facilities provided by the UCL Cosmoparticle Initiative.