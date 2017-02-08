# citus-ansible
Ansible playbook to deploy a citus cluster

Playbooks
=========

* install-9.6.yml : install postgresql cluster

* first-database.yml : create a database and configure citus in it

* citus.yml : activate citus on master node


Howto
=====

Add to you inventory file two section, one called `master` for the
master node, and one called `worker`

Launch the playbook

`$ ansible-playbook -i hosts.ini install-9.6.yml`

`$ ansible-playbook -i hosts.ini first-database.yml`

`$ ansible-playbook -i hosts.ini citus.yml`


Check the install
=================

Connect on the master and execute

`$ psql -d citus -c "SELECT * FROM master_get_active_worker_nodes();"`


What the playbook do
====================

* set up the pgdg debian repo https://wiki.postgresql.org/wiki/Apt

* install postgresql-9.6 with contrib package

* install the citus package

* install python psycopg2 librarie for ansible purpose

* activate citus shared librarie

* configure the clusters to be ready to use

* create a first database called `citus` and activate citus extension
  in it

Tested on
=========

* Debian Jessie

Warning
=======

This is for test purpose only, for a production use you **must**
secure the connection with another method than **trust** in your
pg_hba.
