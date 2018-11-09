# Quorum Examples

This repository contains setup examples for Quorum.

## Getting Started
We will run 7nodes example by running a preconfigured Vagrant environment which comes complete with Quorum, Constellation, Tessera and the 7nodes example (__works on any machine__).

### Base environment


### Setting up Vagrant
1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
2. Install [Vagrant](https://www.vagrantup.com/downloads.html)
3. Download and start the Vagrant instance (note: running `vagrant up` takes approx 5 mins):

    ```sh
    git clone https://github.com/jpmorganchase/quorum-examples
    cd quorum-examples
    vagrant up
    vagrant ssh
    ```

4. To shutdown the Vagrant instance, run `vagrant suspend`. To delete it, run
   `vagrant destroy`. To start from scratch, run `vagrant up` after destroying the
   instance.

