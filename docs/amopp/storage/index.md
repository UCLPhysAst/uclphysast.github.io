---
title: Storage Explained
---

# Storage Explained
There are five types of storage for use on all nodes except for gateway nodes (sometimes referred to as jump boxes) which only have access to the home directory.

<!-- ## [Scratch](scratch.md)
## [Void Store](void.md)
## [Silos](silos.md)
## [Projects Folder ](moon.md) -->

???+ Home Directory

    Located in /home/<username>

    This directory is your home folder. All your user files, personal settings, customizations will be saved in this folder. This folder is network aware and will travel with you regardless of which node you connect to.

    !!! warning
        Do not store personal files (non work/research related content) on these systems such as your music, personal photos/videos etc.


???+ Scratch

    Located in /scratch

    This is located on every compute node. The purpose of this space is to be used to store running/active simulations temp data. If you need to store the results of the processed data, please consider moving it to either void for durations up to six (6) months or the silos for long term storage. 
    
    !!! warning
        Data stored here will also be moved to #Void storage if used for a period of 30 days.


???+ Void Store

    Located in /nfs/void

    This will act as network based scratch storage. This space has very little redundancy and will act as a funnel for data removed from node scratch space. Data will stored for a minimum of six (6) months before it flagged for deletion.


???+ Silos

    Located in /nfs/silo

    This is protected raid storage. This is to be used for long term storage of active projects. Data stored in this space is not subject to any system action, however any data inactive for a period of two (2) years will be flagged and marked for review by the group/project managers/Pi.


???+ Projects Folder

    Located in /nfs/projects

    This is protected raid storage. This will be used for archived projects. This space, data and its usage will be at the sole direction of the project managers/PI's.