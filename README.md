
# Ansible Role - potos\_callrestic

This role works for me, but does not satisfy the potos acceptance rules yet:

* the automated checks are currently failing
* meta is not up to date

This role

* downloads the restic go binary from github and
* installs two wrapper scripts and
* an argos script (if `potos_argos` is also used)

The `call_restic` script allows to use an external medium (like an
USB stick) as backup medium for the `HOME` directory with
[`restic`](https://github.com/restic/restic). The mandatory,
randomly generated encryption key is stored in plain text
in `$HOME/.config/resticpw` and protects
the data on the external medium.

**NOTE:** You absolutely need to make a (safe) copy of this password
to a different place. Without that password, you cannot access the
data on your medium.

## Example Playbook

As this role is tested via Molecule one can use [that
playbook](./molecule/default/converge.yml) as a starting point:

```yaml
---

- name: Converge
  hosts: all
  gather_facts: yes
  tasks:
    - name: run role
      ansible.builtin.include_role:
        name: 'ansible-role-potos_template'
```

## Role Variables

The default variables are defined in [defaults/main.yml](./defaults/main.yml):

```yaml
potos_callrestic_binary: https://github.com/restic/restic/releases/download/v0.16.4/restic_0.16.4_linux_amd64.bz2
```

Another option is to use `ansible-doc` to read the argument specification:

```sh
ansible-doc --type role -r . main ansible-role-potos_callrestic
```

## Requirements

* ansible-role-potos_argos

## License

See [LICENSE](./LICENSE)

## Author Information

[Project Potos](https://github.com/projectpotos)

