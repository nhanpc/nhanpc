LXC Introduction
================

`LXC <https://en.wikipedia.org/wiki/LXC>`_ (LinuX Container), widely knew by `Docker <https://en.wikipedia.org/wiki/Docker_(software)>`_ (a high level API for LXC), are common those days in many applications
like CIs, test, developments and event on Production. GCP, AWS and many cloud provider are support their container flatform due to its securities and isolated properties.

This article will arm to give a basic view of LXC, docker compare to traditional VMs.

Defines
-------

LXC
~~~

**LXC** (LinuX Container) is an operating system-level virtualization through a virtual environment that has its own process and network space
, LXC relies on the Linux kernel `cgroups <https://en.wikipedia.org/wiki/Cgroups>`_ functionality.

LXC inherit Cgroups powers so LXC can have:

    * **Resource limiting**: *Groups can be set to not exceed a configured memory limit*
    
    * **Prioritization**: *Some groups may get a larger share of CPU utilization or disk I/O throughput*
     
    * **Accounting**: *Measures a group's resource usage*
     
    * **Control**: *Freezing groups of processes, their checkpointing and restarting*

LXC is light, it's request a minim resources (memory, CPUs) to run and blast speed. It can boot up in seconds compare to minutes of traditional VMs.
But LXC can only host Linux guest

LXC's securities compare to VMs are cons, because it isn't a real VMs, all processes are run directly on same Linux kernel.

Docker
~~~~~~

VMs
~~~

Compares
~~~~~~~~

+---------------+----------+----------+----------+
|               | LXC      | Docker   | VMs      |
+===============+==========+==========+==========+
| Weigh         | Light    | Light    | Heavy    |
+---------------+----------+----------+----------+
| Snapshot      | FileOnly | FileOnly | Yes(full)|
+---------------+----------+----------+----------+
| Securities    | High     | High     | VeryHigh |
+---------------+----------+----------+----------+

References:
-----------
* https://en.wikipedia.org/wiki/LXC
* https://en.wikipedia.org/wiki/Cgroups
* https://en.wikipedia.org/wiki/Docker_(software)