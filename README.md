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
Note that Vagrant syncs the `vagrant-pimatic-dev` (on the host machine) with `/vagrant` (on the guest machine) so you can use your IDE from the host machine for development.

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

## Tips
Most of the times I find myself opening a second terminal window to keep track of the `pimatic-daemon.log` file:

```bash
$ tail -f /vagrant/vagrant-pimatic-dev/pimatic-daemon.log
```

`tail -f` keeps refreshing and restarting pimatic has no effect on the tail.

### Develop your plugin against Pimatic GitHub repo
The `bootstrap.sh` installs pimatic from the NPM repository. This means some files that are available in the pimatic GitHub repository are not available (for example the Gruntfile is missing in the pimatic NPM module). Here's how to clone pimatic from GitHub:

```bash
$ cd /vagrant/vagrant-pimatic-dev/node_modules
$ rm -rf pimatic/
$ git clone https://github.com/pimatic/pimatic.git

# Don't forget to install the dependencies
$ cd /node_modules/pimatic
$ npm install
```

For more information on pimatic development, read the [pimatic development](http://pimatic.org/guide/development) guide.
