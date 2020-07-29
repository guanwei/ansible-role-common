# Ansible Role: Common

Set common settings on RedHat/CentOS, Debian/Ubuntu or Windows/Windows Core.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```
# Custom hosts entries to be added
# example:
# hosts_entries:
#   - ip_address: 192.168.1.100
#     canoncial_name: foo
#     aliases:
#       - bar
#       - zed
hosts_entries: []

# Proxy settings
# example:
# http_proxy: http://myuser:mypassword@px01.example.com:3128
# https_proxy: http://px01.example.com:3128
# ftp_proxy: http://proxy.example.com:8080
# no_proxy: example.com,192.168.122.1
default_no_proxy: 127.0.0.1,localhost,.local,.internal
# yum_proxy: http://proxysrv:8080
# yum_proxy_username: myuser
# yum_proxy_password: mypassword
# win_inet_proxy: proxy.example.com:8080
# win_inet_bypass:
#   - server1
#   - server2
#   - <-loopback>
#   - <local>

disable_selinux: false
disable_firewalld: false
```

`hosts_entries` will be added to `/et/hosts` file on Linux.
`hosts_entries` will be added to `%windir%\system32\drivers\etc\hosts` file on Linux.

`http_proxy`、`https_proxy`、`ftp_proxy`、`no_proxy` will be added to `/etc/environment` and `/etc/profile.d/proxy.sh` file on Linux.
`http_proxy`、`https_proxy`、`ftp_proxy`、`no_proxy` will be added to `Machine Environment` on Windows.

if one of `http_proxy`、`https_proxy`、`ftp_proxy` set, but `no_proxy` not set,`default_no_proxy` will be used as `no_proxy`.

`http_proxy`、`https_proxy`、`ftp_proxy` will be added to `/etc/apt/apt.conf.d/01proxy` file on Debian/Ubuntu.
`yum_proxy`、`yum_proxy_username`、`yum_proxy_password` will be added to `/etc/yum.conf` file on RedHat/CentOS.

`win_inet_proxy`、`win_inet_bypass` will set IE proxy and WinHTTP proxy.

## Dependencies

None.

## Example Playbook

requirements.yml
```
- name: common
  src: https://github.com/guanwei/ansible-role-common.git
  version: dev
  scm: git
```

playbook.yml
```
- hosts: servers
  roles:
    - common
```
