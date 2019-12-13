# Vagrant environment for DB2 Server and Puppet Enterprise

Creates a Puppet Enterprise server vm and an Agent vm that receives DB2 Server managed by Puppet.

## Pre-requisites

- Vagrant
- Oscar vagrant plugin
- SSHFS vagrant plugin
- VirtualBox
- db2-puppet-control-repo

## Setup

This Vagrant environment uses the SSHFS (SSH Filesystem) Vagrant plugin to mount several directories from the host into the VMs.

```
    synced_folders:
      - host_path: '.'
        guest_path: '/vagrant'
        type: sshfs
      - host_path: '../puppet-control-repo'
        guest_path: '/puppet-control-repo'
        type: sshfs
      - host_path: '../puppet-modules'
        guest_path: '/puppet-modules'
        type: sshfs
```

You will need to have the db2-puppet-control-repo checked out into the parent directory of this Vagrant env, and have a `puppet-modules` directory in the parent also, that has the `crayfishx/db2` module and it's dependencies installed into it, eg:

```
/Users/jesse/src/puppet/projects/db2/puppet-modules
├── crayfishx-db2 (v1.3.1)
├── puppet-archive (v1.3.0)
└── puppetlabs-stdlib (v4.25.1)
```

Putting that together:

```
src/puppet/projects/db2
├── puppet-modules
│   ├── db2
│   ├── archive
│   └── stdlib
├── puppet-control-repo
│   └── ...
└── vagrant_db2_oscar
    └── ...
```

