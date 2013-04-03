# Keyring

A suckless keyring build upon [pass].

## Why?

I was bored feeding my [SSH-Agent] with all my SSH-keys particularly
their passphrases. Because of that i needed a tool which allows me
to add plenty of keys with a sigle passphrase. Just what a keyring does.
Furthermore it has to fit well into my environment and toolchain because
[Gnome-Keyring] and friends just displeases me because of all their
dependencies.

Right! Keyring tries to solve a nibble of beggary.


## Install

Keyring depends on [GnuPG], [OpenSSH] and [pass] a suckless password manager.

### Sources With Symbolic Links

This is the preferred method, because it's easier to track updates and to
contribute.

    cd ~/foo
    git clone https://git.christoph-polcin.com/keyring/
    cd ~/bin
    ln -s ~/foo/keyring/keyring

### Quick & Dirty Drop-In Style

    curl https://git.christoph-polcin.com/keyring/plain/keyring -o ~/bin/keyring
    chmod 700 ~/bin/keyring


## Setup

### Basic Keyring Configuration

Put the following lines into a shell resource file which gets sourced one time,
eg. `~/.zlogin`, `~/.bash_login`, `~/.profile`, `~/.xinitrc`, ...

    eval `keyring --eval --add ~/.ssh/foo_key ~/.ssh/bar_key ~/.ssh/baz_key`

If you need Your keys in every shell session put the following line into
Your default resource file, eg. `~/.bashrc´, `~./.zshrc`, ...

    eval `keyring --eval`

Below are all customizable environmental variables with their default values:

    GPG_INFO_FILE="/tmp/gpg-agent-info.$USER"
    SSH_INFO_FILE="/tmp/ssh-agent-info.$USER"
    PASS_KEY_PREFIX='keyring'

And here is an example how to adjust and submit those values.

    eval ` \
    PASS_KEY_PREFIX='foo' \
    keyring --eval`

### Your Keyring Database

To initialize the password store follow the instructions on the [pass] homepage
or consider their [examples]

Use this naming convention to add your keyring keys / passphrases into [pass] manager,
replace uppercase words. `PASS_KEY_PREFIX` is assigned with `keyring`

    pass insert PASS_KEY_PREFIX/PRIVATE_KEY_FILE_NAME

To add a SSH-key with the default PREFIX and which is located
in `~/.ssh/my-private-ssh-key` use:

    pass insert keyring/my-private-ssh-key

The passprahse which [pass] is asking for has to be the passphrase
of the inserted key.

To unlock the keyring You have to use the passphrase which is assigned with
Your GPG-ID.


## License

Simplified BSD License / FreeBSD License. See LICENSE for details.


## Contributors

- You?


## Notes

Backup and encrypt Your ~/.ssh directory:

    tar -cj .ssh | gpg --symmetric --cipher-algo aes256 --output /tmp/ssh-backup.bz2.gpg

[examples]:         http://git.zx2c4.com/password-store/about/#EXTENDED%20GIT%20EXAMPLE
[SSH-Agent]:        https://en.wikipedia.org/wiki/Ssh-agent
[GnuPG]:            http://www.gnupg.org/
[OpenSSH]:          http://www.openssh.org/
[pass]:             http://zx2c4.com/projects/password-store/
[Gnome-Keyring]:    https://live.gnome.org/GnomeKeyring
