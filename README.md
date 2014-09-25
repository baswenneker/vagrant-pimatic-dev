# vagrant-pimatic-dev
`vagrant-pimatic-dev` creates and configures a portable, reproducible and lightweight virtual development environment for pimatic. It enables cross-platform development of pimatic and pimatic plugins.

## Installation
First, make sure you have the latest version of [Vagrant](http://www.vagrantup.com/downloads.html) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads) installed.

Then, do: 
```bash
$ git clone https://github.com/baswenneker/vagrant-pimatic-dev.git
$ cd vagrant-pimatic-dev
$ vagrant up
```

This will download a virtual machine image and start a bootstrap process that installs node.js and pimatic-dev. Running `vagrant up` for the first time will take a while so go grab a coffee.

## Post installation
You should add these options to the settings section of your `config.json` to get debug outputs:

```json
"debug": true,
"logLevel": "debug"
```

Additionally, change the password or replace the username and password by `"enabled": false` to develop without being asked for credentials:

```json
"authentication": {
    "enabled": false
}
```

## Usage
Note that Vagrant syncs the `vagrant-pimatic-dev` (on the host machine) with `/vagrant` (on the guest machine) so you can use your IDE from the host machine to develop code.

To launch pimatic, execute the folowing (from the `vagrant-pimatic-dev`):

```bash
$ cd <vagrant-pimatic-dev-folder>

# If not done already, do a vagrant up
$ vagrant up 

# The following command sshs into the vagrant virtual machine.
$ vagrant ssh

# Go to the pimatic-dev folder and start the pimatic daemon:
$ cd /vagrant/pimatic-dev
$ sudo node_modules/pimatic/pimatic.js start
```

Then point your browser on the host machine to [http://localhost:4567](http://localhost:4567) for the web-interface. Please keep in mind that the `Vagrantfile` contains a rule that maps port 80 from the guest machine to port 4567 on the host machine.

For more information on pimatic development, read the [pimatic development](http://pimatic.org/guide/development) guide.




