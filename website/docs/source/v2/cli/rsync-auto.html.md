---
page_title: "vagrant rsync-auto - Command-Line Interface"
sidebar_current: "cli-rsyncauto"
---

# rsync-auto

**Command: `vagrant rsync-auto`**

This command watches all local directories of anj
[rsync synced folders](/v2/synced-folders/rsync.html) and automatically
initiates an rsync transfer when changes are detected. This command does
not exit until an interrupt is received.

The change detection is optimized to use platform-specific APIs to listen
for filesystem changes, and does not simply poll the directory.

## Machine State Changes

The `rsync-auto` command does not currently handle machine state changes
gracefully. For example, if you start the `rsync-auto` command, then
halt the guest machine, then make changes to some files, then boot it
back up, `rsync-auto` will not attempt to resync.

To ensure that the command works properly, you should start `rsync-auto`
only when the machine is running, and shut it down before any machine
state changes.

You can always force a resync with the [rsync](/v2/cli/rsync.html) command.

## Vagrantfile Changes

If you change or move your Vagrantfile, the `rsync-auto` command will have
to be restarted. For example, if you add synced folders to the Vagrantfile,
or move the directory that contains the Vagrantfile, the `rsync-auto`
command will either not pick up the changes or may begin experiencing
strange behavior.

Before making any such changes, it is recommended that you turn off
`rsync-auto`, then restart it afterwards.
