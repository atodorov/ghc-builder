Setup a F26 VM for building ghc packages.

 * create-vm
   This will create a new vm using the builder.ks kickstart and an Anaconda boot.iso
   A new ssh key will be generated and embedded in the kickstart and the system will be created.
   builder.ssh and builder.ssh.pub are the ssh keys. builder.ks.in is the kickstart.
   Run it like so: `create-vm ghc-builder /path/to/a/boot.iso`
   At the end it should print the IP address of the VM, if not you can get it using:
   `sudo virsh domifaddr ghc-builder`

 * build-ghc
   This will build the ghc packages on the VM and and gather up all the results.
   Run it like so: `build-ghc <IP ADDRESS>`

 * `push-ghc`
   This will push the results to a remote system. Currently only Amazon S3 is supported.
   `~/.s3cfg` is the default configuration file. `AWS_ACCESS_KEY` and `AWS_SECRET_KEY`
   environment variables may be used to override the defaults.
   Run it like so: `./push-ghc <S3_BUCKET_NAME>`


VM NETWORK PROBLEMS

Some VM setups don't work as expected. If the VM isn't getting an IP the install won't
work. Debugging using VNC will be required.

Try switching the --network=network:default line to --network=bridge:br0 to see if
that works. If that's the case then virsh domifaddr won't work and you will need to
log in to find the IP address.

*NOTE* If you use bridge:br0 CHANGE THE ROOT PASSWORD. It will be on the LAN and you
don't want to leave it set to 'redhat'.

