# Ansible role - EL Patching

[![License](https://img.shields.io/github/license/voidquark/el_patching)](LICENSE)

Apply OS patches on Enterprise Linux machines (e.g. RHEL, CentOS, Rocky, Alma, Fedora ). You can decide which patching method you want to use. There are 3 methods:

- `all` - Apply all patches on target host
- `security` - Apply only security patches on target host
- `bugfix` - Apply only bugfix patches on target host

**I strongly advise visit blog post for detailed information and my recommendation. - BLOG POST SOON**

## Requirements

Only dnf must be available on target machine.

## Role Variables

- **Default Variables**. Usually there is no need to change this but rather overwrite value in `host_vars` or `group_vars` if required.

| Variable Name  | Default Value | Description
| ----------- | ----------- | ----------- |
| `el_patching_required_packages` | `"yum-utils"` | It is required to install yum-utils as this role verify reboot with `needs-restarting`.
| `el_patching_auto_reboot` | `false` | By default do not reboot target host. Only verify if reboot is required.
| `el_patching_reboot_timeout` | `600` | By default auto reboot is disable but default timeout value is set to 5minutes. Value is in `seconds`.
| `el_patching_method` | `"security"` | By default apply only `security` patches on target host. Possible values `"security"/"bugfix"/"all"`
| `el_patching_check_mode` | `false` | By default do not run tasks in check mode. You can enable check mod to simulate patching and reboot.

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