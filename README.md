# Vagrant examples

![alt text](https://blog.web-apps.tech/content/images/size/w2000/2017/12/vagrant-1.png)

## Table of Contents
* [Base Ubuntu 20.04](#Ubuntu-20.04)
* [Syncing a local directory to a Vagrant box](#synced-folder)
* [Naming the VM](#Naming-the-VM)
* [Resource Management](#Resource-Management)
* [Environment Variables](#Environment-Variables)


## Ubuntu 20.04
Create a "box" - VM  
```vagrant init ubuntu/focal64```  

Starts the selected VM   
```vagrant up```  

Make changes to the VM  
```vagrant provision```  

SSH into the VM  
```vagrant ssh```  

Stop a VM  
```vagrant halt```

Teardown/Destroy a VM  
```vagrant destroy```

## synced-folder
To have an updating synced folder/directory to a Vagrant VM add a single line  
to the Vagrantfile. In this below example, data/ exists at the same level as  
Vagrantfile. Any changes made in data/ will be seen in the running VM
```
Vagrant.configure("2") do |config|
  ...
  config.vm.synced_folder 'data/', '/home/vagrant/data'
  ...
end
```

## Naming the VM  
Without naming the VM in the Vagrantfile it will automatically be called "default"  
To give your VM a name add the following inside your Vagrantfile  
```
Vagrant.configure("2") do |config|
  ...
  # Server 1
  config.vm.define "sandbox" do |s1|
    s1.vm.hostname = "sandbox"
  end
  ...
end
```

## Resource Management  
Declaring how many CPUs and how much memory to allocate to your VM can be done  
in the Vagrantfile. Add the following to the file
```
Vagrant.configure("2") do |config|
  ...
  # set resource limit for VM
  config.vm.provider :virtualbox do |v|
    v.memory = 2
    v.cpus = 4096
  end
  ...
end
```

## Environment Variables  
To make the Vagrantfile environment variable friendly, we can use the Vagrant  
plugin called vagrant-env. To install the plugin, run:  
```vagrant plugin install vagrant-env```  
With the plugin we can use a .env file at the same level as our Vagrantfile. Then  
we can use variables like so:  
```
MASTERS_CPU=2
MASTERS_MEM=4096
```
These variables can be used in the Vagrantfile now 
```
Vagrant.configure("2") do |config|
  ...
  # set resource limit for VM
  config.vm.provider :virtualbox do |v|
    v.memory = ENV['MASTERS_MEM']
    v.cpus = ENV['MASTERS_CPU']
  end
  ...
end
```


