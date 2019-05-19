# nutanix-rest-api
Creates consistent VMs via Nutanix REST API calls

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

```
git clone git@github.com:jedioncrk/nutanix-rest-api.git
```

### Prerequisites

What things you need to install the software and how to install them

- Nutanix cluster setup
- Cluster admin bot user
- Define base image via ISO, preferably with cloud-init enabled (CentOS 7 in my case)
- Define networks in Nutanix

## Define Nutanix Cluster(s)

Enter the hostname of the cluster address of Nutanix as a list under the nutanixcluster variable in group_vars/all.yml.

## Cluster Admin User

Create an admin bot user so that REST API calls can authenticate.  Define these variables:

```
nutanix_username: "nutanixbot"
nutanix_pwd: "nutanix4/u"
```

Encrypt the credentials

```
ansible-vault encrypt vault-password-file.yml
```

## Define Base Image

Upload an ISO to the Nutanix Image.  I use CentOS 7 minimal in this case, but you can use your preferred ISO.
Create a VM and go through a base install of the ISO.  Enable cloud-init and any required modules.
Find the vmdisk's UUID by logging into Nutanix CVM via ssh.

```
ssh nutanixc1 -l nutanixbot
acli vm.disk_get <name of VM>
```

Enter the vmdisk's UUID into group_vars/all.yml under the nutanix.vmdisk as a list.  This should match with the cluster list.

## Define Networks

Find the network's UUID by logging into Nutanix CVM via ssh.

```
ssh nutanixc1 -l nutanixbot
acli net.list
```
Enter the network's UUID into group_vars/all.yml.

## Authors

* **David Peng** - *Initial work*

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

