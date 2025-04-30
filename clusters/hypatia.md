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

### Cosmoparticle hardware

The cosmoparticle hardware is overseen by PIs of the relevant grants which enabled its purchase. Potential users should ask their supervisor/line manager whether they may be able to gain access.

## Access

Login is by SSH to hypatia-login.hpc.phys.ucl.ac.uk.

## Using the cluster

Hypatia runs the Rocks 7.0 Linux distribution and uses Slurm as a job manager. 

The home area has total capacity of about 9TB, which is backed up nightly. Although this has a decent amount of space, please minimise usage of it in order to help with backups and keep space free for new users. Alternative storage areas are described below. The home area is also the slowest tier of storage on Hypatia (although still quite fast).

If you are unfamiliar with HPC environments and using batch submissions to run tasks please contact Edd for advice.

