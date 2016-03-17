.. revealjs:: HA Openstack Ops

    James Beedy
    3/17/2016

    Presentation

    `https://github.com/jamesbeedy/os-ha-meetup-present <https://github.com/jamesbeedy/os-ha-meetup-present>`_

    Associated Materials

    `https://github.com/jamesbeedy/os_ha_test_stack <https://github.com/jamesbeedy/os_ha_test_stack>`_

.. revealjs:: About Me

    Cloud Engineer, Dark Horse Comics

    Sys admin, net admin, storage admin, hacker, stacker

    Ubuntu, Debian, FreeBSD, OpenStack, etc

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
 :title-heading: h3

  .. rst-class:: fragment

      Openstack, Big data stacks, web applications!

      Abstract from cfgmgmt --> save cycles!

      Model complex environments!

      Replicable environments across heterogeneous providers!

      Use cfgmgmt tools (chef, puppet, ansible) underneath!

      Write charms in any language!

      Openstack charms Now developed under the Big Tent!


.. revealjs:: Why Openstack HA?
 :subtitle: Must have openstack service resiliency

  .. rst-class:: fragment

  .. list-table::

   * - Maintanence
   * - 0 Down time
   * - Release Upgrades


.. revealjs:: All Openstack services can be HA!
 :title-heading: h2
 :subtitle: Different techniques can/should be used for each type of service
 :subtitle-heading: h4

  .. rst-class:: fragment

      * - Stateless services
        - API endpoints
        - Schedulers
        - Service Agents

      * - Stateful Services
        - Messaging queues
        - Databases
        - Storage


.. revealjs:: Lets start small
 :subtitle: presentation





.. revealjs:: Example Juju Openstack Bundle

   .. image:: _images/l3_ha_bundle.png
    :width: 600
    :height: 550
    :target: https://raw.githubusercontent.com/jamesbeedy/os-ha-meetup-present/master/source/_images/l3_ha_bundle.png
    :alt: l3_ha_bundle


.. revealjs:: Juju Status View

   .. image:: _images/wjst.png
    :width: 600
    :height: 550
    :target: https://raw.githubusercontent.com/jamesbeedy/os-ha-meetup-present/master/source/_images/wjst.png
    :alt: juju_status_view

.. revealjs:: Juju Gui View

   .. image:: _images/juju_gui.png
    :width: 700
    :height: 550
    :alt: juju_gui_view
    :target: https://raw.githubusercontent.com/jamesbeedy/os-ha-meetup-present/master/source/_images/juju_gui.png


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



.. revealjs:: Future Plans

  * Teststack for openstack upgrades
  * Revise webapps to be juju deployed
  * Implement NFV
  * Ceph SAN
  * Find most effective scale out solutions DB/Webapp/Infra

.. revealjs:: Questions?


  `@jamesbeedy <http://twitter.com/jamesbeedy>`_

  `github <http://github.com/jamesbeedy>`_

  `bdx on irc`
