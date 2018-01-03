Ok so this thing here is a WIP and you shouldn't even use it for a demo right now. 

## Proxy
By default the proxy settings are turned off. If you need to fight with a proxy, enable and configure it in the Vagrantfile. It's defined at the top:
```
$proxy = false		# true or false
$proxy_url = "http://proxy.com:port"	# enter proxy URL here!
```


Start your VMs with a simple "vagrant up", afterwards you'll have 4 running VMs not knowing each other very good.
Run the following to enable hostnames, install docker and kubernetes components:

```
vagrant ssh kube-boss # "ubu" is the password by default
..
sudo -i
ansible-playbook -i /vagrant/ansible/inventories/dev/dev.ini /vagrant/ansible/install.yml
..
watch kubectl get nodes
```

the kubernetes components will be installed like this:
- kubectl on kube-boss
- kubelet and kubeadm everywhere (kube-boss, kube-1, kube-2, kube-3)

todos:
- kill proxyfuckups while using kubeadm
- repair userfuckup in vagrantbox: https://bugs.launchpad.net/cloud-images/+bug/1569237 
- add some healthchecks
- be much more generic!

As you might have noticed, this is just the beginning. I'm trying to make it as generic as possible but I'm no ansible hero so this might take a while. The goal is to have the ability to run it on any relevant platform (ARM (Raspberry), x64 etc...). Long way to go from here :)