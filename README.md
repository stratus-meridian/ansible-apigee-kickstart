Ansible playbook for [Apigee Developer Portal Kickstart][1]


## Running the playbook

```shell
$ cp variables.yml.example variables.yml
  # customize the variables within variables.yml

$ cp inventory.ini.example inventory.ini
  # use the vagrant specific inventory example as a starting point
  # for definiting target hosts

$ ansible-playbook -i inventory.ini playbook.yml
```


## Testing locally

Ensure you have local definitions of variables.yml and inventory.ini. By copying the
.example files provided guarantees they will run out of the box locally.

### Vagrant

With vagrant, virtualbox and ansible available locally, a local test environment can be
spun up with: `vagrant up --provider virtualbox --provision`

At the end the Apigee installation wizard should be accessible on http://localhost:8080

### Molecule

*Be sure that the vagrant box is not running while you run the molecule test, as both
spin up a VM with binding local port on 8080*

```shell
$ pip3 install --user molecule
$ pip3 install --user molecule-vagrant

$ molecule test
```

We have to use vagrant with molecule as with the default docker containers there are
certain systemd commands that don't work inside containers (like systemctl daemon-reload).

Because of this, for the GitHub Action runner we have to use macos-latest instead of
ubuntu-latest, as the later does not support virtualization. See https://github.com/actions/virtual-environments/issues/183

[1]: https://www.drupal.org/docs/8/modules/apigee-developer-portal-kickstart/use-kickstart-with-apigee-edge-for-private-cloud
