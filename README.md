
# rhel-lab
Test lab setup for preparing for the Red Hat RHCSA/RHCE exams. Inspired by the VM's provided with the book [Red Hat RHCE/RHCSA 7 Cert Guide](http://www.sandervanvugt.com/books/ "Red Hat RHCE/RHCSA 7 Cert Guide") written by Sander van Vugt  and the real deal on the actual exam. Forked from [All Your Code](https://bitbucket.org/allyourco_de/rhel-lab/overview). 

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
Edit hosts file [as seen here](https://www.howtogeek.com/howto/27350/beginner-geek-how-to-edit-your-hosts-file/).
