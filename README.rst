deployments.buildout.ucarp
==========================

This is a buildout for managing an high availability cluster using ucarp_

Requirements
------------

Debian/Ubuntu::

    apt-get install ucarp

RedHat/CentOS::

    yum install ucarp

Minimal configuration
---------------------

On your master node:

    * extend/edit master.cfg to specify:

        - ucarp.conf:vip_address
        - ucarp.conf:source_address (current node physical ip)

On your backup node:

    * extend/edit backup.cfg to specify:

        - ucarp.conf:vip_address
        - ucarp.conf:source_address (current node physical ip)

Many parameters can be modified, check base.cfg and the template you want to
use.

**RedHat/CentOS** users may want to modify builoudt:parts
to use **ucarp.redhat.conf**.

High availability
------------------

Master node: use master.cfg
Backup node: use backup.cfg

Each node is identified by a physical ip.
A third virtual ip is assigned by the ucarp_ daemon

Usually the virtual ip is assigned to the master node.
If master goes down the backup node will claim the virtual ip.

To force the the virtual ip assignment to the backup node,
e.g. for releasing upgrades or maintainance,
you can stop the ucarp daemon on the master node::

 [root@master ~]# /etc/init.d/ucarp stop

The master node will get the virtual ip back
if you restart the ucarp daemon on **both nodes**::

 [root@master ~]# /etc/init.d/ucarp start

 [root@backup ~]# /etc/init.d/ucarp restart


.. _ucarp: http://www.pureftpd.org/project/ucarp
