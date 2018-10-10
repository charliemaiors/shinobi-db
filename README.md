Shinobi DB
=========

This role will deploy Mariadb, configure it, and create and populate the schema for [Shinobi CCTV](https://shinobi.video/).
Ubuntu 18.04/16.04, CentOS 7 and Archlinux are supported. 

Requirements
------------

This role has no requirements.

Role Variables
--------------

The role requires the definition of four variables:

```yaml
user_mail: "mail@example.com"
user_pass: "password"
shinobi_pass: "password"
```

User related variables (```user_mail``` and ```user_password```) define to the real user on the shinobi frontend. Shinobi variable (```shinobi_pass```), instead, is the password for database connection of the backend service.
The default variables are:

```yaml
shinobi_user: "shinobi"
dbhash: "md5"
mysql_root: "supersecurerootpassword"
```

plus a third variable used for random password generation. The ```shinobi_user``` variable represent the authorized user with grants on ccio database for shinobi. The ```dbhash``` variable is the hashing algorithm for ```user_pass``` variable on db, in order to be compliant with the recent [update](https://gitlab.com/Shinobi-Systems/Shinobi/commit/b7a3317aac6665c71a6d74140c2e5bae906aca78) on shinobi platform; the allowed values are:

* md5
* sha256
* sha512

Mariadb root password (defined with ```mysql_root``` variable)is the password for the root user.
All password variables if are undefined will be generated random (and printed in the ansible log). 

Example Playbook
----------------

This role could be used defining only user mail, leave as default the hashing algorithm and random generation for all passwords.

```yaml
    - hosts: servers
      roles:
         - { role: shinobi-db, user_mail: "ccio@m03.ca" }
```

Or you could define your own passwords and select a proper hash algorithm.

```yaml
- hosts: servers
  roles:
      - { role: shinobi-db, user_mail: "ccio@m03.ca" user_password: "test", shinobi_password: "test", mysql_root: "supersecurerootpassword", dbhash: "sha256" }
```

License
-------

GNU GPL

Author Information
------------------

This role was created in 2018 by Carlo Maiorano as developer for Dipartimento di Informatica - Scienza e Ingegneria of Alma Mater Studiorum directed and supervisioned by Paolo Bellavista as Group Leader.
