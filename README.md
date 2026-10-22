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
| `redis.conf_path` | `/etc/redis` | Directory the role writes `<port>.conf` into |
| `redis.port` | `6379` | Port set in the generated config, also used as its file name |
| `redis.db_path` | `/var/lib/redis` | Parent of the data directory (`<db_path>/<port>`) in the generated config |
| `redis.pid_path` | `/var/run/redis` | Directory for the pid file (`<pid_path>/<port>.pid`) in the generated config |

`redis` is a single map, so overriding it replaces all four keys.

The generated `<conf_path>/<port>.conf` is not read by the packaged `redis-server` service, which uses `/etc/redis/redis.conf`. Redis runs with the package defaults (port 6379, bound to localhost).

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
