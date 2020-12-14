CI Badge

# Ansible role for libvirt kickstart installs
Runs virt-install to kickstart a host

## Example usage
```yaml
- hosts: localhost
  gather_facts: no
  vars_prompt:
    name: root_password
    prompt: Give me the root password
    private: yes
    confirm: true
    encrypt: sha512_crypt
  roles:
    - role: ansible-role-libvirt-kickstart
      vars:
        libvirt_host: vmhost
        virt_install_location: https://ftp.funet.fi/pub/linux/mirrors/centos/8.3.2011/BaseOS/x86_64/kickstart/
        centos_mirror_root: https://ftp.funet.fi/pub/linux/mirrors/centos/
        vm_name: vmtest1.exmple.com
        libvirt_network: ovs-trunk0,portgroup=vm
        libvirt_data_dir: /storage/vm/images
        consistent_interface_naming: false # default
        vm_interface: "eth0" # default
        vm_type: centos8 # see templates/
        vm_ip_address: '10.1.1.3'
        vm_netmask: 255.255.255.0
        vm_gateway: 10.1.1.1
        vm_nameserver: 10.1.1.1
```

## Getting started
Ensure all dependencies are installed and then follow the below process
1. `git clone repo` Get the development repository
2. `pre-commit install` Install the pre-commit hooks
3. Make edits as explained in the customization section
4. `pre-commit` Make sure existing code is good
5. `do development` Dont ask me :D
6. `pre-commit` Make sure the edits are good to go
7. `molecule converge`

## Dependencies
This repo expects 3 things installed on the local machine
1. [pre-commit](https://pre-commit.com/) Methodology to test yaml style
2. [ansible-lint](https://github.com/ansible-community/ansible-lint) lint ansible code for best practices
3. [yamllint](https://github.com/adrienverge/yamllint) Ensures all yaml is well formed

### Customization
There are a few files that are required to be updated when using this template
1. [molecule/requirements.yml](molecule/requirements.yml) - Update with any required  roles or collections
2. [molecule/default/converge.yml](molecule/default/converge.yml) - update with new role name
3. [molecule/default/molecule.yml](molecule/default/molecule.yml) - update with desired distributions and extra playbooks

### Optional
The github actions are configured to automatically run the molecule tests but if you want to load them locally you will also need molecule installed on the development machine

## Advanced
There are numerous other options within the [defaults/main.yml](./defaults/main.yml) that can change other parts of the behavior of the system

## Changelog
The [changelog](./CHANGELOG.md) is stored externally
