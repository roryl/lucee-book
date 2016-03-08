# Vagrant

For simple development tasks, CommandBox provides an [embedded development server](https://rorylaitila.gitbooks.io/lucee/content/lucee_server.html) which is easy to get started, however it is not suitable for running production servers. If you want to develop locally with a full VM that mirrors your production environment, [Vagrant](https://www.vagrantup.com) is a useful tool for this. 

Vagrant simply wraps a [VirtualBox VM](https://www.virtualbox.org/wiki/Downloads) and provides easy to use networking and file synchronization between your development environment and the VM. It also provides hooks for scripting automated setups of your environment. 

##Sample Vagrant File

This vagrant file cane be used to configure a Lucee VM. This article does not go into the specific of using Vagrant, for that follow a [Vagrant Tutorial](https://www.vagrantup.com/docs/)