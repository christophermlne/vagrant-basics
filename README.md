# vagrant-basics
Shell provisioner to create a base box for Rails development

Currently provisions a box that includes:  
* Ruby 2.1.5
* rbenv
* git
* bundler
* rails
* nodejs
* vim

May eventually include:
* nginx set up to reverse proxy
* postgres 9.3
* ??

##Instructions
Clone this repo and then run ```$ vagrant up```
Use Vagrant to package the VM then register it as a vagrant box to use as the basis for other projects...
