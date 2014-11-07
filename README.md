# Hypernode test environment for MacOSX and Linux

## Starting the test environment

1. Install Virtualbox 4.3.18 or later.
2. Install Vagrant 1.6.4 or later.
3. Clone this [repository](https://github.com/ByteInternet/hypernode-vagrant.git) using Git or download the [tarball](https://github.com/ByteInternet/hypernode-vagrant/archive/master.zip) from Github.

```
cd hypernode-vagrant
vagrant plugin install vagrant-vbguest vagrant-hostmanager
vagrant up
```

## Using the test environment

### Uploading files

The local directories `data/web/public/` and `data/web/nginx/` are bound to the Vagrant image. You can use this local dir to edit all your files.

So fire up PHPStorm and edit away locally. Then check out the Hypernode box to see results.

### Webserver

Your Magento is available at [http://127.0.0.1:8080](http://127.0.0.1:8080).

### MySQL

MySQL is available at 127.0.0.1 port 3307.

### SSH

SSH is available on 127.0.0.1 port 2222.

You can use `ssh -p 2222 app@localhost` to connect to SSH. You can also use this config snippet for SSH:

```
Host hn-vagrant
    Hostname 127.0.0.1
    User app
    Port 2222
    StrictHostKeyChecking no  # because the host key will change over time
```

To connect directly from the vagrant directory you can use `vagrant ssh`. This will log you in as the `vagrant` user.
It will allow you to use `sudo` and manage the server. The app user should be used for normal usage and as the website user.

## Keeping up to date with Hypernode versions

With every Hypernode release, we'll update the Hypernode vagrant image as well. Use the following to update your box (you'll lose your MySQL data unless you make a mysqldump first!):

```bash
vagrant box update
# optionally backup MySQL, whose data is not currently in a shared directory
vagrant destroy
vagrant up
```

## Customizing the setup

You might have some ports already in use. Hypernode by default forwards ports 2222 to 22, 3307 to 3306 and 8080 to 80.

If you want to change these ports, just have a look at the Vagrant file. It is pretty self-explanatory.

## Troubleshooting

### ==> default: stdin: is not a tty

This is Vagrant bug [#1673](https://github.com/mitchellh/vagrant/issues/1673) and perfectly harmless.
