# Quorum Examples

This repository contains setup examples for Quorum.

## Getting Started
We will run 7nodes example by running a preconfigured Vagrant environment which comes complete with Quorum, Constellation, Tessera and the 7nodes example (__works on any machine__).


### Setting up Vagrant
1. Install [Git](https://git-scm.com/download/win)
2. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
3. Install [Vagrant](https://www.vagrantup.com/downloads.html)
4. Download and start the Vagrant instance (note: running `vagrant up` takes approx 5 mins) using git bash:

    ```sh
    $ git clone https://github.com/jpmorganchase/quorum-examples
    $ cd quorum-examples
    $ vagrant up
    $ vagrant ssh
    ```
    
5. To shutdown the Vagrant instance, run `vagrant suspend`. To delete it, run
   `vagrant destroy`. To start from scratch, run `vagrant up` after destroying the
   instance.
6. Install constellation

    ```sh
    $ ls
    $ tar vxf constellation-0.3.2-ubuntu1604.tar.xz 
    $ sudo cp -r constellation-0.3.2-ubuntu1604 /usr/local/bin/
    ```


### Run 7nodes example
1. inital and start the 7nodes

    ```sh
    $ cd quorum-examples/7nodes
    $ ./raft-init.sh
    $ ./raft-start.sh
    ```

2. Get the node you want(dd1 is node1)
    
    ```sh
    $ geth attach ipc:qdata/dd1/geth.ipc
    ```

3. Sending a transaction(Open another terminal)

    ```sh
    $ cd quorum-examples
    $ vagrant ssh
    $ cd quorum-examples/7nodes
    $ ./runscript.sh private-contract.js
    ```
    You will get a TransactionHash here, copy it
    
4. Check the transaction(back to node1's terminal)

    ```sh
    > eth.getTransaction("TransactionHash")
    ```
    You can see the information of the transaction

5. See the privacy of node(Open three terminal for node1, node4, node7)
    In node1
    ```sh
    > var address = "0x1932c48b2bf8102ba33b4a6b545c32236e342f34";
    > var abi = [{"constant":true,"inputs":[],"name":"storedData","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"x","type":"uint256"}],"name":"set","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"get","outputs":[{"name":"retVal","type":"uint256"}],"payable":false,"type":"function"},{"inputs":[{"name":"initVal","type":"uint256"}],"type":"constructor"}];
    > var private = eth.contract(abi).at(address)
    ```
    For node1, node4, node7
    ```sh
    > private.get()
    ```
    
    You should see node1, node7 get 42 and node4 get 0 because node4 have no permission to see the privacy transaction
    
###Resources
1.jpmorganchase/quorum-examples: Examples for Quorum[https://github.com/jpmorganchase/quorum-examples]
2.Quorum─JP Morgan基於Ethereum打造的聯盟鏈[https://blog.lizen.me/quorum-jp-morgan/]
