# Ansible role - EL Patching

[![License](https://img.shields.io/github/license/voidquark/el_patching)](LICENSE)

Apply OS patches on Enterprise Linux (RHEL) and other Red Hat derivatives (e.g. CentOS, Rocky, Alma, Fedora). You can decide which patching method you want to use. There are 3 methods:

- `all` - Apply all patches on target a host
- `security` - Apply only security patches on target a host
- `bugfix` - Apply only bugfix patches on target a host

**I strongly advise visiting the blog post for detailed information and my recommendation. - BLOG POST SOON**

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
| `el_patching_check_mode` | `false` | By default task is not executed in check mode. You can enable check mode to simulate patching and reboot. Keep in mind that check mode can't predict if a reboot is required.

## Dependencies

No Dependencies

## Example Playbook

Create the following playbook.
```yaml
- name: Apply OS Patches
  hosts: your_patching_inventory_group_or_host
  become: true
  roles:
    - el_patching
```

## License

MIT

## Author Information

Created by [VoidQuark](https://voidquark.com)
