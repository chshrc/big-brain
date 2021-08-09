On Debian-based distributions the default home permissions of newly created user accounts are set by applying the `umask` rule 022 (meaning: strip all permissions from group and others) resulting in the permissions 755.
This means, that every user can view and execute files on any other users' home directory.
Red Hat-based distributions differ here by having `UMASK` set to 077 in `/etc/login.defs`. This way, newly created user home directories are set with 700 permissions.

> The `UMASK` rule is set in the above mentioned file `/etc/login.defs` on Debian-based distributions, but on Red Hat-based distros I have yet to find out, where 022 is set.
