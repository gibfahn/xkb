# My xkb remapping

I use this repo to manage my Ubuntu key remapping.

## How to use

See what I do in my setup:

For full instructions, see
[what I do in my setup](https://github.com/gibfahn/dot/blob/ed33ca7b9e7a0ad6f9e73f3cec902399208aeea7/setup/ubu.sh#L83-L98)
(you probably want the same section in that repo's master branch).


Basically you want to put this git repo in `/usr/share/X11/xkb/` without
overwriting the files in that directory. Changes won't take effect till you
overwrite the temp files (see last step of bash script) so experiment away.

```bash
# Not required, but I cba to `sudo git` everywhere.
sudo chown -R $USER:`id -gn` "$XKB"
pushd /usr/share/X11/xkb

# Git init and git add rather than clone to avoid overwriting.
git init
git remote add up git@github.com/gibfahn/xkb.git
git fetch --all
git reset up/master

# Check whether my master matches what's in your distro.
git status --porcelain

# IMPORTANT: if `git status --porcelain` has output, don't do the next steps
# until you understand why! Continue at your own risk.

# Checkout my branch.
git checkout gibLayout

# Deletes and regenerates the files in `/var/lib/xkb/*.xkm`.
sudo dpkg-reconfigure xkb-data
```

## Inspiration

- https://medium.com/@damko/a-simple-humble-but-comprehensive-guide-to-xkb-for-linux-6f1ad5e13450
