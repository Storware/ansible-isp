IBM Spectrum Protect Server
=========

This role deploys IBM Spectrum Protect Server for Kodo for Endpoints

Requirements
------------

CentOS Stream/RHEL 8 minimal installation and public key authentication between command host and target machine

Role Variables
--------------

Defaults:
```
---
isp_server_version: "8.1.12.000"
isp_short_version: "{{ isp_server_version | regex_replace('([0-9]+)[.]([0-9]+)[.]([0-9]+)[.].*', 'v\\1r\\2') }}"
isp_server_installer_filename: "{{ isp_server_version }}-IBM-SPSRV-Linuxx86_64.bin"
isp_server_download_url: "http://ftp.software.ibm.com/storage/tivoli-storage-management/maintenance/server/{{ isp_short_version }}/Linux/{{ isp_server_version }}/x86_64/{{ isp_server_installer_filename }}"
isp_server_installer_local_dir: "/tmp/isp"
isp_server_installer_local_path: "{{ isp_server_installer_local_dir }}/{{ isp_server_installer_filename }}"
iim_dir: "/opt/IBM/InstallationManager/eclipse"
iim_shared_dir: "/opt/IBM/IBMIMShared"
isp_dir: "/opt/tivoli/tsm"
isp_limits_file: "/etc/security/limits.d/21-isp.conf"
isp_port: 1500
isp_port_ssl: 1501
isp_instance_name: "tsminst1"
isp_server_name: "isp1"
isp_user: "{{ isp_instance_name }}"
isp_uid: 1111
isp_user_home: "/home/{{ isp_user }}"
isp_server_service_script_template_path: "{{ isp_dir }}/server/bin/dsmserv.rc"
isp_group: "tsmadmin"
isp_data_dir: "/isp"
isp_data_fs_type: "xfs"
isp_data_mkfs_opts: "-K"
isp_data_resizefs: true
isp_data_fs_mount_opts: "defaults,inode64"
isp_instance_path: "{{ isp_data_dir }}/{{ isp_instance_name }}"
isp_db_disk: "/dev/sdb"
isp_db_path: "{{ isp_data_dir }}/db"
isp_db_fs_type: "{{ isp_data_fs_type }}"
isp_db_mkfs_opts: "{{ isp_data_mkfs_opts }}"
isp_db_resizefs: "{{ isp_data_resizefs }}"
isp_db_fs_mount_opts: "{{ isp_data_fs_mount_opts }}"
isp_activelog_disk: "/dev/sdc"
isp_activelog_path: "{{ isp_data_dir }}/activelog"
isp_activelog_fs_type: "{{ isp_data_fs_type }}"
isp_activelog_mkfs_opts: "{{ isp_data_mkfs_opts }}"
isp_activelog_resizefs: "{{ isp_data_resizefs }}"
isp_activelog_fs_mount_opts: "{{ isp_data_fs_mount_opts }}"
isp_archlog_disk: "/dev/sdd"
isp_archlog_path: "{{ isp_data_dir }}/archlog"
isp_archlog_mkfs_opts: "{{ isp_data_mkfs_opts }}"
isp_archlog_resizefs: "{{ isp_data_resizefs }}"
isp_archlog_fs_type: "{{ isp_data_fs_type }}"
isp_archlog_fs_mount_opts: "{{ isp_data_fs_mount_opts }}"
isp_dbbackup_disk: "/dev/sde"
isp_dbbackup_path: "{{ isp_data_dir }}/dbbackup"
isp_dbbackup_fs_type: "{{ isp_data_fs_type }}"
isp_dbbackup_mkfs_opts: "{{ isp_data_mkfs_opts }}"
isp_dbbackup_resizefs: "{{ isp_data_resizefs }}"
isp_dbbackup_fs_mount_opts: "{{ isp_data_fs_mount_opts }}"
isp_dbbackup_maxcap: "50G"
isp_dbbackup_devclass: "dbbackup"
isp_dbbackup_schedule: "{{ isp_dbbackup_devclass }}"
isp_dbbackup_script: "{{ isp_dbbackup_devclass }}"
isp_dbbackup_script_template_path: "dbbackup.script.mac.j2"
isp_storage_disks:
  - "/dev/sdf"
isp_storage_paths:
  - "{{ isp_data_dir }}/storage1"
isp_storage_fs_type: "{{ isp_data_fs_type }}"
isp_storage_mkfs_opts: "{{ isp_data_mkfs_opts }}"
isp_storage_resizefs: "{{ isp_data_resizefs }}"
isp_storage_fs_mount_opts: "{{ isp_data_fs_mount_opts }}"
isp_stgpool_name: "bdata"
isp_domain: "kodo"
isp_mgmtclass: "kodo-nolimit"
isp_policyset: "{{ isp_domain }}"
isp_create_extra_mgmt_classses: true
isp_extra_mgmt_classses:
  - name: "7days"
    vere: "7"
    verd: "7"
    rete: "nolimit"
    reto: "nolimit"
  - name: "30days"
    vere: "30"
    verd: "30"
    rete: "nolimit"
    reto: "nolimit"
isp_schedule_dbbackup: "10:00"
isp_schedule_expire: "17:00"
isp_dbmgropt_servername: "TSMDBMGR"
isp_db_activelogsize: 32768
isp_admin_user: "tsmadmin"
isp_admin_pass: "passw0rd"
isp_admin_pass_exp: 0
isp_setopt_template_path: "setopt.mac.j2"
isp_setopt_actlogretention: "30 m=d"
isp_setopt_expinterval: 0
isp_setopt_maxsession: 999
isp_setopt_deduprequiresbackup: no
isp_setopt_dnslookup: no
isp_setopt_commtimeout: 360
isp_setopt_idletimeout: 360
isp_setopt_allowreorgtable: yes
isp_setopt_allowreorgindex: yes
isp_setopt_reorgbegintime: "06:00"
isp_setopt_reorgduration: 4
isp_setopt_clientdeduptxnlimit: 2048
isp_setopt_serverdeduptxnlimit: 2048
isp_setopt_deduptier2filesize: 1024
isp_setopt_deduptier3filesize: 9999
isp_setopt_dateformat: 3
isp_setopt_numopenvolsallowed: 50
isp_setopt_backupinitiationroot: "off"
isp_create_service_node: true
isp_service_node_name: "storware"
isp_service_node_password: "St0rw@re"
isp_service_node_maxnump: 100
isp_service_node_dedup: "client"
dsmadmc: "source ~/.bashrc && dsmadmc -id={{ isp_admin_user }} -pa={{ isp_admin_pass }}"
db2icrt_bin: "{{ isp_dir }}/db2/instance/db2icrt"
db2ilist_bin: "{{ isp_dir }}/db2/bin/db2ilist"
```

Key variables:

* `isp_server_download_url` - - URL to be used to download ISP server (download may be slow,
so you can also download it manually, upload it to the remote machine and set this variable
to something like `file:///tmp/8.1.12.000-IBM-SPSRV-Linuxx86_64.bin` which will copy installer from local
* `iim_dir` - IIM installation directory
* `iim_shared_dir` - IIM shared directory
* `isp_dir` - ISP installation directory
* `isp_instance_name` - ISP server instance name
* `isp_server_name` - ISP server name
* `isp_user` - service user name for ISP server
* `isp_uid` - UID of service user name for ISP server
* `isp_user_home` - home directory of service user name for ISP server
* `isp_group` - user group for service user name for ISP server
* `isp_data_dir` - root directory for ISP mountpoints
* `isp_data_fs_type` - file system type used to create all ISP file systems
* `isp_data_mkfs_opts` - mkfs options for default file system used to create all ISP file systems
* `isp_data_resizefs` - option to automatically resize filesystems to the available space
  (if the block device has changged between playbook invocations)
* `isp_data_fs_mount_opts`: mount options for default file system used to create all ISP file systems
* `isp_instance_path` - ISP server instance directory
* `isp_db_disk` - block device used for ISP database
* `isp_db_path` - mount point used for ISP database
* `isp_db_fs_type` - file system type for ISP database
* `isp_db_mkfs_opts` -  mkfs options for the file system for ISP database
* `isp_db_resizefs` - option to automatically resize filesystem for ISP database to the available space
  (if the block device has changged between playbook invocations)
* `isp_db_fs_mount_opts` - mount options for the file system for ISP database
* `isp_activelog_disk` - block device used for ISP active log
* `isp_activelog_path` - mount point used for ISP active log
* `isp_activelog_fs_type` - file system type for ISP active log
* `isp_activelog_mkfs_opts` - mkfs options for the file system for ISP active log
* `isp_activelog_resizefs` - option to automatically resize filesystem for ISP active log to the available space
  (if the block device has changged between playbook invocations)
* `isp_activelog_fs_mount_opts` - mount options for the file system for ISP active log
* `isp_archlog_disk` - block device used for ISP archive log
* `isp_archlog_path` - mount point used for ISP archive log
* `isp_archlog_fs_type` - file system type for ISP archive log
* `isp_archlog_mkfs_opts` -  mkfs options for the file system for ISP archive log
* `isp_archlog_resizefs` - option to automatically resize filesystem for ISP archive log to the available space
  (if the block device has changged between playbook invocations)
* `isp_archlog_fs_mount_opts` - mount options for the file system for ISP DB backups
* `isp_dbbackup_disk` - block device used for ISP DB backups
* `isp_dbbackup_path` - mount point used for ISP DB backups
* `isp_dbbackup_fs_type` - file system type for ISP DB backups
* `isp_dbbackup_mkfs_opts` - mkfs options for the file system for ISP DB backups
* `isp_dbbackup_resizefs` - option to automatically resize filesystem for ISP DB backups to the available space
  (if the block device has changged between playbook invocations)
* `isp_dbbackup_fs_mount_opts` - mount options for the file system for ISP DB backups
* `isp_dbbackup_maxcap` - max. capacity for ISP DB backups
* `isp_dbbackup_devclass` - device class name for DB backup
* `isp_dbbackup_schedule` - schedule name for DB backup
* `isp_dbbackup_script` - script name for DB backups
* `isp_dbbackup_script_template_path` - path to the template of the macro defining DB backup script - if you want to change script definition
* `isp_storage_disks` - list of block devices to be used for storage pool
* `isp_storage_paths` - list of mountpoints for storage pool
  * must be the same length as `isp_storage_disks`)
  * each storage path corresponds to one block device in the `isp_storage_disks` lists
* `isp_storage_fs_type` - file system type for ISP storage pool
* `isp_storage_mkfs_opts` - mkfs options for the file system for ISP storage pool
* `isp_storage_resizefs` - option to automatically resize filesystem for ISP storage pool to the available space
  (if the block device has changged between playbook invocations)
* `isp_storage_fs_mount_opts` - mkfs options for the file system for ISP storage pool
* `isp_stgpool_name` - storage pool name
* `isp_domain` - domain name
* `isp_mgmtclass` - management class name
* `isp_policyset` - policyset name
* `isp_create_extra_mgmt_classses` - flag if additional management classes should be defined
* `isp_extra_mgmt_classses` - list of management class definitions - each one must have `name`, `vere`, `verd`, `rete`, `reto` parameters provided
* `isp_schedule_dbbackup` - time at which ISP DB backup job should start
* `isp_schedule_expire` - time at which ISP data expiration job should start
* `isp_db_activelogsize` - active log size
* `isp_admin_user` - ISP admin user name
* `isp_admin_pass` - ISP admin password
* `isp_admin_pass_exp` - ISP admin password expiration (days)
* `isp_setopt_template_path` - path to the alternative script for setting base options using `setopt` command
* `isp_create_service_node` - flag to create service node for other services (such as Kodo) should be created
* `isp_service_node_name` - service node name created for other services (such as Kodo) should be created
* `isp_service_node_password` - service node password
* `isp_service_node_maxnump` - maximum number of mount points a service node can use, at one time
* `isp_service_node_dedup` - deduplication setting for the service node

Dependencies
------------

N/A

Example Playbook
----------------

This deploys Kodo server on `server` host (only one server can be deployed)
and multiple agents on `agents` hosts

```
- hosts: isp
  roles:
   - xe0nic.ansible_isp_server
```

Example hosts inventory (you need to make sure that SSH public key authentication for
ansible user provided in inventory is configured):

```
[all:vars]
ansible_user = root

[isp]
192.168.155.233
```

License
-------

MIT

Author Information
------------------

For more information visit product website: https://storware.eu/products/kodo-for-endpoints
Documentation: https://storware.gitbook.io/kodo-for-endpoints