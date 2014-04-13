# vagrant-sshfs

A Vagrant plugin to mount a folder from the box to the host using sshfs.

## Why

Common solutions for sharing folders with Vagrant include synced folder, which is pretty slow when dealing with many files, and NFS. NFS didn't work for me because of encrypted disk restrictions. An alternative was to mount a folder in the host machine pointing the a folder in the box with sshfs.

## Installation

`vagrant plugin install vagrant-sshfs`

## Usage

In the `Vagrantfile`, add a configuration like this:

`config.sshfs.paths = { "src" => "mountpoint" }`

`src` is the source absolute path to the folder in the box, `mountpoint` is the folder in the host machine. `mountpoint` can be an absolute path, or relative to the `Vagrantfile`.

By default it will use the Vagrant ssh username. You can change that with the following:

`config.sshfs.username = "theusername"`

## Issues

### Connection reset by peer

In case you are getting "Connection reset by peer" errors, it might be the case that you already have a host configuration under your `~/.ssh/know_hosts` for the given ip, and you are using the same ip with a different machine. If that is the case, you can set a `StrictHostKeyChecking no` under that ip to skip the check:

```
Host 127.0.0.1
StrictHostKeyChecking no
```

## Contributing

If you have issues or ideas, please contribute! You can create an issue throught Github, or send a Pull Request.

## Development

To try this out, you can run `bundle exec vagrant up` from the source code checkout.
