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

 * push-ghc
   This will push the results to a remote system. TBD.

