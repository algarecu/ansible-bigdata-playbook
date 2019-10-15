# citus-ansible
Ansible playbook to deploy a citus cluster

Playbooks
=========

* ansible-bigdata-playbook.yml : install postgresql cluster + extensions

* config-database.yml : create a database and configure citus in it

* citus.yml : activate citus on master node


Built using
=========

* ubuntu version trusty64

Howto
=====

Add to you inventory file two section, one called `master` for the
master node, and one called `worker`

Launch the playbook in the master server

`$ ansible-playbook -i hosts.ini ansible-bigdata-playbook.yml`

`$ ansible-playbook -i hosts.ini config-database.yml`

`$ ansible-playbook -i hosts.ini citus.yml`


Check the install
=================

Connect on the master and execute

`$ psql -d citus -c "SELECT * FROM master_get_active_worker_nodes();"`


What the playbook do
====================

* set up the pgdg debian repo https://wiki.postgresql.org/wiki/Apt

* install postgresql-11 with contrib package

* install the citus package

* install python psycopg2 librarie for ansible purpose

* activate citus shared library

* configure the clusters to be ready to use

* create a database called `citus` and activate citus extension
  in it

Vagrant (test on a local network)
=======

* vagrant init
* Edit the .Vagrantfile
* vagrant up
* vagrant status


Warning
=======

This is for test purpose only, for a production use you **must**
secure the connection with another method than **trust** in your
pg_hba.
