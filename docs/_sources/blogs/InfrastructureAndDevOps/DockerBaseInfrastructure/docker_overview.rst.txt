Docker Overview
***************

`Docker <https://en.wikipedia.org/wiki/Docker_(software)>`_ is a "containerization" program, 
which is provide `operating-system-level virtualization <https://en.wikipedia.org/wiki/Operating-system-level_virtualization>`_.

Those days , Docker are widely used in many applications, include **serverless application** and **Continuous integration** (CI) due to
the ability of create **isolated**, **securities** and **lightweight** environments for each container.

Run first Docker's container instance
=====================================

Docker is easy to run everywhere with simple command :code:`$ docker up [option] [dockerimage]` then your instance is ready.

Eg : Run an instance of Wordpress: ::

    $ sudo docker run -d --name wordpress -p8080:80 wordpress

.. todo::

    Explain docker's options: name, port ...

Now point your web-browser to :code:`http://localhost:8080/` and enjoy your Wordpress instance without Apache, PHP and MySQL install.

Monitor your containers resources
=================================

To use docker building-in resources monitor command: ::
  
    $ sudo docker stats

Result sill be some things like this: ::

    CONTAINER ID        NAME                CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
    7d78cb0276ff        wordpress           0.00%               25.62MiB / 6.813GiB   0.37%               60.8kB / 70.8kB     14.4MB / 0B         9

Now you see the magic here, Wordpress's container just take ~25.6MiB of RAM, compare to a mini VM to run a LAMP stash must take ~400MiB of RAM...

.. todo::

    Explain ``docker stats`` command output

Hundred to Thousands replica on single machine
==============================================

We are going to create 100 (one hundred) instance of Wordpress on different ports:

::

    start=`date +%s`
    number_of_instance=100
    
    for i in `seq 1 $number_of_instance`
    do
        port=$(( 7000 + $i ))
        sudo docker run -d --name wordpress_$i -p$port:80 wordpress
    done

    end=`date +%s`
    exec_time=$((end-start))
    echo $exec_time 

It just take ~100 seconds to script executed.

Now run ``docker stats`` and see the resources taken by them, it's a very very small resource they taken, just like a process. 
That's because `Docker container's architecture <#id1>`_.

.. hint:: To remove containers created by last script:

    ::

        number_of_instance=100
        
        for i in `seq 1 $number_of_instance`
        do
            port=$(( 7000 + $i ))
            sudo docker stop wordpress_$i && docker rm wordpress_$i
        done

Docker container's architecture
===============================

.. figure:: /_static/images/blogs/InfrastructureAndDevOps/DockerBaseInfrastructure/Blog.-Are-containers-..VM-Image-1.png

+---------------------+----------------------+----------------------+
|                     | Docker               | VMs                  |
+=====================+======================+======================+
| Weigh               | Light                | Heavy                |
+---------------------+----------------------+----------------------+
| Snapshot            | FileOnly             | Yes(full)            |
+---------------------+----------------------+----------------------+
| Securities          | High                 | VeryHigh             |
+---------------------+----------------------+----------------------+
| Different OS (1)    | NO                   | YES                  |
+---------------------+----------------------+----------------------+

References:
===========
* https://en.wikipedia.org/wiki/LXC
* https://en.wikipedia.org/wiki/Cgroups
* https://en.wikipedia.org/wiki/Docker_(software)
* https://robin.io/blog/containers-deep-dive-lxc-vs-docker-comparison/
* https://docs.docker.com/engine/docker-overview/
