---
layout: post
title: Stuck in a Ubuntu Login Loop
date: 2020-02-23
---

Ubuntu apparently has a known bug throughout various versions of sticking people in a login loop, wherein the incorrect password is objected to but a correct password loops back to the user-select screen. The immediate answer, according to most sources, is that `Xauthority`, a graphics file, has an incorrect user/permission set.

-   from login screen, go into terminal with `ctrl + alt + f2`
-   check permissions with `ls -lah | grep -i Xauthority` (specific flags to look for the hidden file)
-   if owner is `root`, change it to the user

Next most likely culprit is the `.tmp` file

-   from terminal, enter `sudo ls -lah /tmp`
-   permissions for `.` should be `drwxrwxrwt`

Neither of those worked for my situation. TIL there's a problem with auto-login on Ubuntu 19.10, which requires the user to update Grub options.

-   Reboot into `recovery mode`
-   Select `root`
-   ```
    mount -o rw,remount /           # get write permission
    sudo nano /etc/default/grub     # edit grub options
    ```
-   remove the word "splash" from the `GRUB_CMDLINE_LINUX_DEFAULT` line
-   `sudo update-grub`

Rebooted, got in, turned off auto login, supposedly everything works again. Keeping fingers crossed.