.. revealjs:: HA Openstack Ops

    James Beedy
    3/16/2016

.. revealjs:: About Me

    Cloud Engineer, Dark Horse Comics

    Sys admin, net admin, storage admin, hacker, stacker

    Ubuntu, Debian, FreeBSD, OpenStack, etc



.. revealjs:: So why Openstack?

  .. rst-class:: fragment

      Large user base, plugable, zero lock in, opensource, trust

      Works great for deployments that need to scale, or virtual laptop labs 

      Needed a flexible and elastic environment for testing, staging

      Projects are requesting more flexible computing resources

      Experience for operators and developers --> larger community ==> stronger/better/safer/faster/reliable software



.. revealjs:: Why Openstack HA?

  .. rst-class:: fragment

     Need openstack service resiliency
     
       *  Maintanence
       *  0 Down time
       *  Upgrades


.. revealjs:: The beginning

  .. rst-class:: fragment

      2009 VMWare - ESXi

      OFA,OVF

      Machine spec templates

      2012 Openstack Essex Release

      Handroll 

      Devstack/vagrant

      Templates

      Chef


.. revealjs:: Juju - Big Software - Modeling
   :title-heading: h2

  .. rst-class:: fragment

      Openstack, Big data stacks, web applications

      Abstract from cfgmgmt --> save cycles

      Model complex environments!!!! ++1 :-)

      Replicable environments accross heterogeneous providers!

      Use cfgmgmt tools (chef, puppet, ansible) underneath!

      Write charms in any language!
      
      Now developed under the Big Tent!
  
    .. __: http://jujucharms.com


.. revealjs:: Webapps and DBS

  .. rst-class:: fragment

      Every webapp needs the same things, usually in different places
      
      Abstract from cfgmgmt --> save cycles

      Automate everything

      Replicable environments accross heterogeneous providers



.. revealjs:: All Openstack services can be configured to be HA!

  .. rst-class:: fragment

      Different services need different HA architectures
          Stateless services
              * API endpoints
              * Schedulers
              * Service Agents

          Statefull Services
              * Messaging queues
              * Databases
              * Storage

              
              
.. revealjs:: All Openstack services can be configured to be HA!
 :title-heading: h2
 :subtitle: Different techniques can be used for each service
 :subtitle-heading: h4

  .. rst-class:: fragment

      Different services need different HA architectures
          * Stateless services
              * API endpoints
              * Schedulers
              * Service Agents

          * Statefull Services
              * Messaging queues
              * Databases
              * Storage


.. revealjs:: Example Juju Openstack Bundle

   .. image:: _images/1.png



.. revealjs:: Deploy MySQL

  .. rv_code::

      $ juju deploy mysql
      $ juju deploy mysql-slave -n2
      $ juju add-relation mysql:master mysql-slave:slave


.. revealjs:: Deploy PostgreSQL Cluster

  .. rv_code::

      $ juju deploy postgresql
      $ juju add-unit postgresql -n2


.. revealjs:: Deploy Percona-cluster - ExtraDB

  .. rv_code::
      
      $ juju deploy percona-cluster -n 3 --config charmconf.yaml
      $ juju deploy hacluster percona-hacluster --config charmconf.yaml
      $ juju add-relation percona-hacluster percona-cluster


.. revealjs:: Deploy MongoDB - Replica Set

  .. rv_code::
      
      $ juju deploy mongodb -n 2
      $ juju add-unit mongodb -n 2


.. revealjs:: Deploy MongoDB Sharded Cluster

  .. rv_code::
      
      $ juju deploy mongodb configsvr --config charmconf.yaml -n3
      $ juju deploy mongodb mongos
      $ juju deploy mongodb shard1 --config charmconf.yaml -n3
      $ juju deploy mongodb shard2 --config charmconf.yaml -n3
      $ juju deploy mongodb shard3 --config charmconf.yaml -n3
      $ juju add-relation mongos:mongos-cfg configsvr:configsvr
      $ juju add-relation mongos:mongos shard1:database
      $ juju add-relation mongos:mongos shard2:database
      $ juju add-relation mongos:mongos shard3:database
              


.. __: http://jujucharms.com
.. __: https://openstack.org
.. __: https://github.com/jamesbeedy

.. revealjs:: Future Plans

  * Teststack for openstack upgrades
  * Revise webapps to be juju deployed
  * Implement NFV 
  * Ceph SAN
  * Find most effective scale out solutions DB/Webapp/Infra 

.. revealjs:: Questions?

  James Beedy

  jamesbeedy@gmail.com

  `@jamesbeedy`_

  https://www.github.com/jamesbeedy/dhc_ops_presentation
  https://www.github.com/jamesbeedy/layer-present

.. _@jamesbeedy: http://twitter.com/jamesbeedy
