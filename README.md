# Ansible Role: Percona

Ansible playbook to install percona MySQL server in Debian/Ubuntu servers

[![Build Status](https://api.travis-ci.org/overdrive3000/ansible-percona.svg)](https://travis-ci.org/overdrive3000/ansible-percona/)

## Requirements

None.

## Role Variables

Available variables are listed below with its default values.

	root_password: reallylongpassword

Define the MySQL root password, this password will be used to create a **/root/.my.cnf** to allow root mysql connections without password

	percona_version: "5.7"
	
Define version Percona, if not defined will be installed "Percona 5.6" by default 

In this release was disabled generation custom config file my.cnf for "Percona 5.6" and "Percona 5.7" (It'll be present in future releases playbook). 
Some settings my.cnf file for "Percona 5.5" see below:

	port: 3306
	bind_address: 0.0.0.0

Define port and bind address for MySQL connections

	max_allowed_packet: 16M
	key_buffer: 16M
	thread_stack: 192K
	thread_cache_size: 8

Define some values to tuning the database server

	sqldebug: true
	log_slow_queries: log_slow_queries    = /var/log/mysql/mysql-slow.log
	long_query_time: long_query_time      = 2
	log_queries_not_using_indexes: log-queries-not-using-indexes


If **create_app_db** is true this playbook will configure an application database, you can set a path for a SQL dump file if you want to restore data in the new application database

## Dependencies

None.

## Example Playbook

	---
	- hosts: all
	  user: vagrant
	  sudo: true
	  vars:
		  - percona_version: "5.7"
		  - db_name: mydb
		  - db_user: myuser
		  - db_host: localhost
		  - db_user_password: mypassword
		  - db_dump_file: /tmp/dump.sql.bz2
	  roles:
		  - overdrive3000.ansible-percona

## License

MIT / BSD

## Notes

This is my first playbook it is a beta version and can be improved, please help me to improve and fix bugs for this playbook.

Thanks.
