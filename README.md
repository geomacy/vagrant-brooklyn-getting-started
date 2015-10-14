# vagrant-brooklyn-getting-started
Vagrant files to bootstrap Apache Brooklyn Getting Started example

## How to use

This assumes you have already installed Virtualbox and Vagrant on your local machine.

The supplied `server.yaml` contains both a Brooklyn node and 3 small BYON nodes, you can ignore the BYON nodes if you only intend to test cloud deployments.

### Starting Brooklyn Node

1. Clone this repo

    ```
    git clone https://github.com/johnmccabe/vagrant-brooklyn-getting-started.git
    ```

2. Cd into the repo and start the brooklyn node

    ```
    cd vagrant-brooklyn-getting-started
    vagrant up brooklyn
    ```

3. Connect to the [Brooklyn Web Console](http://localhost:8081/)

### Starting BYON Nodes

1. From the repo directory you can start the BYON nodes with. (Note that you can add additional nodes to `server.yaml` if desired)

    ```
    vagrant start byon1 byon2 byon3
    ```

2. They will be availble to add to your blueprint with the following location

    ```
    location:
      byon:
        user: vagrant
        password: vagrant
        hosts:
          - 10.10.10.101
          - 10.10.10.102
          - 10.10.10.103
    ````