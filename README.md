# lvmsnapback

## Description

The `lvmsnapback` script is based on the theories of:  

* Mike Ruebel's [Easy Automated Snapshot style Backups with Linux & Rsync](http://www.mikerubel.org/computers/rsync_snapshots/)  
* [snapback2](https://github.com/gitpan/Snapback2)
* Added LVM2 copy-on-write concepts for incremental Backups

## Dependencies
`lvmsnapback` makes use of [hashfyre/yamlparser](https://github.com/Hashfyre/yamlparser) script to parse it's config file `lvmsnapback.conf`

## Usage

```shell
Usage:
  lvmsnapback
      ( --logical-volume | -L ) < LVM volume >
      ( --remote-host | -H ) < remote host name >

# On the remote host
# For storing daily incremental backup hardlinks
sudo mkdir -p /datadrive/snapshot_backups Mon Tue Wed Thu Fri Sat Sun
```

## Configurations

The `lvmsnapback` script can be extended with the provided `lvmsnapback.conf`  
as follows:  

```YAML
---
today: `date +%a`
yesterday: `date --date yesterday +%a`
vol_group: 'name of the volume group'
rsync_user: 'rmote user account for rsync'
rsync_user_key: /home/${rsync_user}/.ssh/id_rsa
ssh_cmd: ssh -i ${rsync_user_key} ${rsync_user}@${remote_host_param}
snap_volume: lv_snapshot_"${today}"
snapshot_root: /tmp/snapshot_mount_"${today}"
config_snapshot_size_in_GB: "size of the snapshot volume"
remote_backup_root: 'path to store snapshot backup file system on the remote host'
log_file: /var/log/lvmsnapback_${today}.log
```

## Contributing

1. Fork the repo
2. Submit a pull request :D

## Author

Joy Bhattacherjee
