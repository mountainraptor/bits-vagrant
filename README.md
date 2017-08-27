# BITS Vagrant

A <a href="https://www.vagrantup.com/" target="_blank">Vagrant</a> configuration focused on creating a stable environment for <a href="https://github.com/LGSInnovations/bits" target="_blank">BITS</a> development.

<!-- MarkdownTOC autolink="true" indent="    " bracket="round" -->

- [Quickstart](#quickstart)
- [Dependencies](#dependencies)
- [Includes](#includes)
- [Optional Includes](#optional-includes)
- [Development Environment](#development-environment)

<!-- /MarkdownTOC -->

## Quickstart

Clone this repo as a sibling directory of BITS

```
.
├── bits
└── bits-vagrant
```

Run `vagrant up` from the `bits-vagrant` directory. Once the provisioning process has completed, run the following:
```bash
vagrant ssh
runbits
```

Navigate to <a href="https://bits.dev:9001" target="_blank">https://bits.dev:9001</a> in your browser.

## Dependencies

* VM provider like <a href="https://www.virtualbox.org/" target="_blank">VirtualBox</a>
* <a href="https://www.vagrantup.com/" target="_blank">Vagrant</a>
* <a href="https://github.com/cogitatio/vagrant-hostsupdater" target="_blank">Vagrant Hostsupdater</a> `vagrant plugin install vagrant-hostsupdater`
* <a href="http://docs.ansible.com/ansible/latest/intro_installation.html#installing-the-control-machine">Ansible</a>

## Includes

* Ubuntu Xenial
* Python 2.7
    * python-crypto
    * python-serial
    * python-netifaces
    * python-magic
* NodeJS 6.x
* Yarn

## Optional Includes

Custom modules will most likely have a need for additional provisioning tasks. These tasks can be placed in the <a href="provisioning/roles/optional/tasks/tasks.d/">`./provisioning/roles/optional/tasks/tasks.d/`</a> directory to be automatically included in the provisioning process. Commonly used tasks are located in <a href="provisioning/roles/optional/tasks/available/">`./provisioning/roles/optional/tasks/available/`</a> and should be symlinked to `tasks.d` if needed.

## Development Environment

Setting up an environment for developing your module(s) is easy. Add an additional sibling directory on the host machine, `modules`, the structure should now look like:

```
.
├── bits
├── bits-vagrant
└── modules
    ├── module-1
    ├── module-2
    └── module-n
```

Uncomment the line `# config.vm.synced_folder "../modules", "/opt/bits-data/base/modules/modules"` in the <a href="Vagrantfile">`Vagrantfile`</a>. If the VM is running, run `vagrant halt`, then run `vagrant up`. Any properly formatted module placed in the host machine's `module` directory will now be automatically loaded by BITS on the remote machine.

Create a symlink from <a href="./provisioning/roles/optional/tasks/available/bits-modules-run-build.yml">`provisioning/roles/optional/tasks/available/bits-modules-run-build.yml`</a> to the <a href="./provisioning/roles/optional/tasks/tasks.d/">`./provisioning/roles/optional/tasks/tasks.d/`</a> directory to have your module(s) be automatically built in the provisioning process.
