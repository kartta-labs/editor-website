# Note for historic-map-stack

This is a customised version of the openstreetmap-website for historic map editing, you'd need to change the instructions to fit with this repository

e.g. https://github.com/historic-map-stack/editor-website

# Installing Vagrant

On Ubuntu, it should be as simple as:

```
sudo apt-get install vagrant
```

Other Linux distributions should have similar installation instructions using `dnf`, `pacman`, or similar.

Installers are available for Mac OS X and Windows, please see the [Vagrant project download page](https://www.vagrantup.com/downloads.html) for more information.

Note than until there are suitable _xenial64_ [vagrant boxes](https://atlas.hashicorp.com/boxes/search?utf8=%E2%9C%93&sort=&provider=&q=xenial64) for other providers,
the only virtualization provider supported is virtualbox. You might need to install it and specify `--provider virtualbox` when setting up your environment.

# Setting up openstreetmap-website

Once Vagrant has been installed, you can start an environment by checking out the openstreetmap-website code if you haven't already, then changing to the directory which contains the Vagrantfile by typing:

```
git clone git@github.com:openstreetmap/openstreetmap-website.git
cd openstreetmap-website
vagrant up
```

This will take a few minutes to download required software from the internet and set it up as a running system. Once it is complete, you should be able to log into the running VM by typing:

```
vagrant ssh
```

Initial set up of secrets. 
If you have been given one, copy the master.key to config/ directory. If you don't have one, just delete the config/credentials.yml.enc file and run 

```
EDITOR="vim" bundle exec rails credentials:edit
```

to edit the `secret_key_base` value. You can keep the credentials.yml.enc file in version control but don't keep the master.key there!

Within this login shell, you can do development, run the server or the tests. For example, to run the tests:

```
cd /srv/openstreetmap-website/
rake test
```

To access the web pages you run the following commands then access the site in your [local browser](http://localhost:3000):

```
vagrant ssh
cd /srv/openstreetmap-website/
rails server --binding=0.0.0.0
```

You edit the code on your computer using the code editor you are used to using, then through shared folders the code is updated on the VM instantly.

You should run the tests before submitting any patch or Pull Request back to the original repository. Please see [CONTRIBUTING.md](CONTRIBUTING.md) for more information.
