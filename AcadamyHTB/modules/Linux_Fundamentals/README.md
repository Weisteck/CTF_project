# Linux Fundamentals

## Sommaire

## Introduction

### Philosophie 

| **Principle**                                                                                                                                                  | **Description**                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Everything is a file`                                                                                                                                         | All configuration files for the various services running on the Linux operating system are stored in one or more text files.                                   |
| `Small, single-purpose programs`                                                                                                                               | Linux offers many different tools that we will work with, which can be combined to work together.                                                              |
| `Ability to chain programs together to perform complex tasks`                                                                                                  | The integration and combination of different tools enable us to carry out many large and complex tasks, such as processing or filtering specific data results. |
| `Avoid captive user interfaces`                                                                                                                                | Linux is designed to work mainly with the shell (or terminal), which gives the user greater control over the operating system.                                 |
| `Configuration data stored in a text file`                                                                                                                     | An example of such a file is the `/etc/passwd` file, which stores all users registered on the system.                                                          |

Le tableau provient de [AcademyHTB](https://academy.hackthebox.eu)

### Fichier Système 

| **Path**                                                                                                                                                                                                                                                                                                                          | **Description**                                                                                                                                                                                                                                                                                                                   |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/`                                                                                                                                                                                                                                                                                                                               | The top-level directory is the root filesystem and contains all of the files required to boot the operating system before other filesystems are mounted as well as the files required to boot the other filesystems. After boot, all of the other filesystems are mounted at standard mount points as subdirectories of the root. |
| `/bin`                                                                                                                                                                                                                                                                                                                            | Contains essential command binaries.                                                                                                                                                                                                                                                                                              |
| `/boot`                                                                                                                                                                                                                                                                                                                           | Consists of the static bootloader, kernel executable, and files required to boot the Linux OS.                                                                                                                                                                                                                                    |
| `/dev`                                                                                                                                                                                                                                                                                                                            | Contains device files to facilitate access to every hardware device attached to the system.                                                                                                                                                                                                                                       |
| `/etc`                                                                                                                                                                                                                                                                                                                            | Local system configuration files. Configuration files for installed applications may be saved here as well.                                                                                                                                                                                                                       |
| `/home`                                                                                                                                                                                                                                                                                                                           | Each user on the system has a subdirectory here for storage.                                                                                                                                                                                                                                                                      |
| `/lib`                                                                                                                                                                                                                                                                                                                            | Shared library files that are required for system boot.                                                                                                                                                                                                                                                                           |
| `/media`                                                                                                                                                                                                                                                                                                                          | External removable media devices such as USB drives are mounted here.                                                                                                                                                                                                                                                             |
| `/mnt`                                                                                                                                                                                                                                                                                                                            | Temporary mount point for regular filesystems.                                                                                                                                                                                                                                                                                    |
| `/opt`                                                                                                                                                                                                                                                                                                                            | Optional files such as third-party tools can be saved here.                                                                                                                                                                                                                                                                       |
| `/root`                                                                                                                                                                                                                                                                                                                           | The home directory for the root user.                                                                                                                                                                                                                                                                                             |
| `/sbin`                                                                                                                                                                                                                                                                                                                           | This directory contains executables used for system administration (binary system files).                                                                                                                                                                                                                                         |
| `/tmp`                                                                                                                                                                                                                                                                                                                            | The operating system and many programs use this directory to store temporary files. This directory is generally cleared upon system boot and may be deleted at other times without any warning.                                                                                                                                   |
| `/usr`                                                                                                                                                                                                                                                                                                                            | Contains executables, libraries, man files, etc.                                                                                                                                                                                                                                                                                  |
| `/var`                                                                                                                                                                                                                                                                                                                            | This directory contains variable data files such as log files, email in-boxes, web application related files, cron files, and more.                                                                                                                                                                                               |


Le tableau vient de [AcademyTHB](https://academy.hackthebox.eu)

## Le Shell

La ligne de commande d'un terminal bash commencera souvent par la structure suivante :
```
<nomUtilisateur>@<nomMachineHote><dossierTravailCourant>
```

RTFM :
```
man <nomCommande>
or
<commande> --help
or
apropos <commande>
```

### Commande basique

| **Command**                                                                                                                        | **Description**                                                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `whoami`                                                                                                                           | Displays current username.                                                                                                         |
| `id`                                                                                                                               | Returns users identity                                                                                                             |
| `hostname`                                                                                                                         | Sets or prints the name of current host system.                                                                                    |
| `uname`                                                                                                                            | Prints operating system name.                                                                                                      |
| `pwd`                                                                                                                              | Returns working directory name.                                                                                                    |
| `ifconfig`                                                                                                                         | The ifconfig utility is used to assign or to view an address to a network interface and/or configure network interface parameters. |
| `ip`                                                                                                                               | Ip is a utility to show or manipulate routing, network devices, interfaces and tunnels.                                            |
| `netstat`                                                                                                                          | Shows network status.                                                                                                              |
| `ss`                                                                                                                               | Another utility to investigate sockets.                                                                                            |
| `ps`                                                                                                                               | Shows process status.                                                                                                              |
| `who`                                                                                                                              | Displays who is logged in.                                                                                                         |
| `env`                                                                                                                              | Prints environment or sets and executes command.                                                                                   |
| `lsblk`                                                                                                                            | Lists block devices.                                                                                                               |
| `lsusb`                                                                                                                            | Lists USB devices                                                                                                                  |
| `lsof`                                                                                                                             | Lists opened files.                                                                                                                |
| `lspci`                                                                                                                            | Lists PCI devices.                                                                                                                 |

Le tableau vient de [AcademyTHB](https://academy.hackthebox.eu)


Pour trouver les variables d'environnement : 
```
env | grep nomVariable
```

##


## Ressources :

* [AcademyHTB](https://academy.hackthebox.eu)
* [Filesystem Hierarchy](https://www.pathname.com/fhs/)
* 