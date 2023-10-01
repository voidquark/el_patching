# Ansible role - EL Patching

[![License](https://img.shields.io/github/license/voidquark/el_patching)](LICENSE)

Apply OS patches on Enterprise Linux (RHEL) and other Red Hat derivatives (e.g. CentOS, Rocky, Alma, Fedora). You can decide which patching method you want to use. There are 3 methods:

- `all` - Apply all patches on target a host
- `security` - Apply only security patches on target a host
- `bugfix` - Apply only bugfix patches on target a host

**I recommend visiting the [blog post](https://voidquark.com/ansible-linux-os-patching/) for detailed information, usage example, and my recommendation.**

## Requirements

Only dnf must be available on the target machine.

## Role Variables

- **Default Variables**. Usually, there is no need to change this but rather overwrite the value in `host_vars` or `group_vars` if required.

| Variable Name  | Default Value | Description
| ----------- | ----------- | ----------- |
| `el_patching_required_packages` | `"yum-utils"` | It is required to install yum-utils as this role verifies reboot with `needs-restarting`.
| `el_patching_auto_reboot` | `false` | By default do not reboot the target host. Only verify if a reboot is required.
| `el_patching_reboot_timeout` | `600` | By default auto reboot is disabled but the default timeout value is set to 5 minutes. Value is in `seconds`.
| `el_patching_method` | `"security"` | By default apply only `security` patches on the target host. Possible values `"security"/"bugfix"/"all"`

- **group_vars** or **host_vars** variables.

| Variable Name | Example Usage | Required | Description
| ----------- | ----------- | ----------- | ----------- |
| `el_patching_exclude_packages` | <pre>el_patching_exclude_packages:<br>&emsp;- tar<br>&emsp;- zip</pre> | No | Exclude packages during patching.

## Dependencies

No Dependencies

## Example Playbook

Create the following playbook.
```yaml
- name: Apply OS Patches
  hosts: your_patching_inventory_group_or_host
  become: true
  roles:
    - voidquark.el_patching
```

## Example execution

- Normal Execution 
```shell
ansible-playbook -i inventory/hosts playbook.yml
```

- If you want to run playbook in check mode
```shell
ansible-playbook -i inventory/hosts playbook.yml --check
```


## License

MIT

## Author Information

Created by [VoidQuark](https://voidquark.com)
