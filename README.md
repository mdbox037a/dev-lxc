# dev-lxc

This is a tidy little Python script I use when I want to quickly create an [LXD system container][1] for development purposes. It mounts the current directory in the home directory of the instance.

## Installation

It's a single script file. Make sure you have [LXD installed][2] and Python 3.10 or higher. Get the file, make it executable, and put it on your `PATH` somewhere.

## Basic Usage

### Create an instance

Create an instance using a specific Ubuntu series, by codename:

    dev_lxc create jammy

You can create multiple instances of the same series in the same directory.

If you have a valid YAML file for configuring the instance (nice for if you want it to start with certain packages installed):

    dev_lxc create jammy --config ./my-config.yaml

### Interacting with existing instances

Use the commands below to interact with your existing instances. You may be prompted to specify which instance to act upon if there are multiple or partial matches for the series you specify.

### Open a shell in an instance

Once you've created an instance, you can spin up a shell in it:

    dev_lxc shell jammy

The default user (`ubuntu`) should be uid-mapped to your user, so file permissions should be okay.

### Exec a command in an instance

    dev_lxc exec jammy 'echo "hello"'

This executes using `bash`, so try not to get too fancy. You can also provide environment variables:

    dev_lxc exec jammy 'echo "hello $MITCH"' --env MITCH="mitchell"

### Stop or Start an instance

    dev_lxc stop jammy

Stops the instance from running. Most other commands (`shell`, `exec`) should start the instance if it's stopped before running.

    dev_lxc start jammy

Starts it up again.

### Remove Instance

    dev_lxc remove jammy

This deletes the instance. It is gone for good.

   [1]: https://canonical.com/lxd
   [2]: https://canonical.com/lxd/install
