# Phansible Role: Redis

[![CI](https://github.com/phansible/role-redis/actions/workflows/ci.yml/badge.svg)](https://github.com/phansible/role-redis/actions/workflows/ci.yml)

An Ansible Role that installs [Redis](https://redis.io/) from the official packages.redis.io apt repository on Ubuntu and Debian, created with [Phansible](http://phansible.com/) in mind.

## Requirements

- Ubuntu 22.04, 24.04, 26.04 or Debian 12, 13 (x86_64)
- Ansible >= 2.15
- Root access or `become` on the target
- HTTPS access to packages.redis.io

## Role Variables

Defaults from `defaults/main.yml`:

| Variable | Default | Description |
| --- | --- | --- |
| `redis.conf_path` | `/etc/redis` | Directory holding the packaged `redis.conf`; the role writes `phansible.conf` there |
| `redis.port` | `6379` | Port Redis listens on, also the name of the data directory |
| `redis.bind` | `0.0.0.0` | Addresses Redis listens on |
| `redis.db_path` | `/var/lib/redis` | Parent of the data directory (`<db_path>/<port>`) |

`redis` is a single map, so overriding it replaces all four keys.

The role writes these settings to `<conf_path>/phansible.conf` and appends `include <conf_path>/phansible.conf` to the packaged `redis.conf`. Redis applies the last occurrence of a directive, so the role's values win over the package defaults and the rest of `redis.conf` stays as packaged.

The packaged `redis-server` unit only allows writes under `/var/lib/redis`, `/var/log/redis`, `/run/redis` and `/etc/redis`, so keep `db_path` under `/var/lib/redis`.

Redis 8 runs with `protected-mode yes`. With no password set it only answers clients on the loopback interface, even when bound to `0.0.0.0`. To reach it from the host, set a password (`requirepass`) or turn protected mode off in `redis.conf`.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - role-redis
```

## License

This role is released under the terms of the license specified in the repository or if not specified, under the [MIT license](https://raw.githubusercontent.com/phansible/role-redis/master/LICENSE).

## Author Information

This role was created in 2015 by [The Phansible Team & Contributors](https://github.com/phansible/role-redis/graphs/contributors), credits go also to [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/) and source of inspiration.
