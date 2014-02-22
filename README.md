# vagrant-postgresql
====================

My Vagrant configuration for Ubuntu 12.04 LTS 64-bit and PostgreSQL 9.3 database.

## Usage

You need to install [omnibus plugin](https://github.com/schisamo/vagrant-omnibus) to ensure that the latest Chef is installed (minimum required version is 11.0):

    vagrant plugin install vagrant-omnibus
    
Then execute the usual:

    vagrant up
    
And you're good to go. Now you have PostgreSQL running on a virtual machine with the default port `5432` mapped outside and ready to accept connections.

Username is `vagrant`, password is `password`, initial db is `vagrant`, but you can change these in Vargant file.

For example you can connect to PostgreSQL with `psql`:

    psql -h localhost -p 5432 -U vagrant vagrant

