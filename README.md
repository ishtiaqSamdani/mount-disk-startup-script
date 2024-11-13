# mount-disk-startup-script.sh.tpl

```
ADDITIONAL_DISK="/dev/disk/by-id/google-${ADDITIONAL_DISK_DEVICE_NAME}" # from terraform
MOUNT_POINT="/mnt/disks/${ADDITIONAL_DISK_DEVICE_NAME}"

# disk formated ? leave : format
/bin/lsblk -fn -o FSTYPE $ADDITIONAL_DISK | grep ext4 || sudo mkfs.ext4 -m 0 -E lazy_itable_init=0,lazy_journal_init=0,discard $ADDITIONAL_DISK

sudo mkdir -p $MOUNT_POINT

sudo mount -o discard,defaults $ADDITIONAL_DISK $MOUNT_POINT

sudo chmod a+w $MOUNT_POINT

echo "$ADDITIONAL_DISK $MOUNT_POINT ext4 discard,defaults 0 2" | sudo tee -a /etc/fstab


```
