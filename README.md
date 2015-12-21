# vagrant-brooklyn-getting-started
Vagrant files to bootstrap [Apache Brooklyn Getting Started example](https://brooklyn.incubator.apache.org/v/latest/start/running.html).

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

3. Connect to the [Brooklyn Web Console](http://10.10.10.100:8081/)

### Starting BYON Nodes

1. From the repo directory you can start the BYON nodes with. (Note that you can add additional nodes to `server.yaml` if desired)

    ```
    vagrant up byon1 byon2 byon3 byon4
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
          - 10.10.10.104
    ````

### View Brooklyn Logs

1. To view logs you must first connect to the brooklyn VM (from the root of this repository):

    ```
    vagrant ssh brooklyn
    ```

2. As Brooklyn is being started by systemd in this VM you can view the logs from the brooklyn unit as follows:

    ```
    sudo journalctl -u brooklyn
    ```
    
    Alternatively you can view them directly in the syslog:

    ```
    sudo tail -f /var/log/syslog
    ```
