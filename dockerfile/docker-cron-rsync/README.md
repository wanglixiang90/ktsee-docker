This image is used for sync code from NFS to local disk, and sync content of user-generated to NFS, every 5 mins.

1. Write a sync shell script named `cron-rsync.sh`, and saved to `/root/rsync`
2. Add volume for source code to `/root/code`, where your code on NFS
3. Add volume for the content of user-generated to `root/upload`, where you want to upload to NFS
4. This image was made by surenkid.

`cron-rsync.sh` example:
```
#!/bin/sh
local_dir=/var/www/html/
code_dir=/root/code/
upload_dir=/root/upload/

# Pull code from remote
rsync -avzhupgo $code_dir $local_dir >> /proc/self/fd/2

# Push user generate content to remote
rsync -avzhupgo --include="upload" --exclude="/*" $local_dir $upload_dir >> /proc/self/fd/2
```