
# rhel-lab
Test lab setup for preparing for the Red Hat RHCSA/RHCE exams. Inspired by the VM's provided with the book [Red Hat RHCE/RHCSA 7 Cert Guide][1] written by Sander van Vugt  and the real deal on the actual exam. Forked from [All Your Code][4]. 

## Description
This will create 3 VM's with, besides the vagrant user, the following users:

User            | Password
----------------|--------
student (wheel) | student
root            | redhat

#### classroom.example.com
* ip: 172.25.0.254
* ipa server: https://classroom.example.com
* cert & keytabs: ftp://classroom.example.com
    - server.keytab is configured for nfs and cifs
* ipa administartor admin with password 'password'
* ipa user lisa with password 'password'
* ipa user linda with password 'password'

#### server.example.com
* ip: 172.25.0.11
* minimal server
* with an extra NIC for teaming
    - ip: 172.25.0.12
* with an extra 10 GiB unpartitioned drive
* added as an ipa-client to the realm EXAMPLE.COM

#### desktop.example.com
* ip: 172.25.0.10
* with an extra 10 GiB unpartitioned drive
* Server with GUI (installed but not enabled)

## Requirements
* Vagrant
* libvirt or VirtualBox (libvirt is preffered. Install vagrant-libvirt plugin)
* Virtualbox or VMWare on Windows (Untested)
* atleast 4 GiB free memory (with recommended settings)
* atleast 20 GiB free storage  (with recommended settings)

## Install

To be able to access the ipa interface at `https://classroom.example.com` you will need to modify your hosts file:
### On Linux
```
echo '172.25.0.254 classroom.example.com classroom' >> /etc/hosts
```
Or else access it via the GUI on the VM `desktop.example.com`

Edit the `Vagrantfile` and modify `config.vm.box`.

Also the following environment variables can be set instead of editing the `Vagrantfile`:
`VBOX_VM_PATH`, `LIBVIRT_STORAGE_POOL`

### CentOS version:

```
cd rhel-lab
vagrant up
```

### On Windows
Edit hosts file [as seen here][3].



<!-- RETAINED FROM ORIGINAL. NOT RECOMMENDED AS RHCSA/RHCE ARE BOTH RHEL 7.0
### RHEL version:
//_Note: The rhel version requires an active subscription._
//
//Download both the **RHEL 7.3 Vagrant box for libvirt or VirtualBox** and the **Red Hat Container Tools** from [access.redhat.com][2].
```
unzip cdk-*.zip && cd cdk/plugins
vagrant plugin install vagrant-registration
vagrant box add rhel/7.3 file://rhel-cdk-kubernetes-*.vagrant-*.box
export SUBSCRIPTION_USERNAME='foo' SUBSCRIPTION_PASSWORD='bar'
cd rhel-lab
vagrant up
```
-->

[1]: http://www.sandervanvugt.com/books/ "Red Hat RHCE/RHCSA 7 Cert Guide"
[2]: https://access.redhat.com/downloads/content/293/ver=2.4/rhel---7/2.4.0/x86_64/product-software "access.redhat.com"
[3]: https://www.howtogeek.com/howto/27350/beginner-geek-how-to-edit-your-hosts-file/
[4]: https://bitbucket.org/allyourco_de/rhel-lab/overview
---
