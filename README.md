# Vagrant Ubuntu Development Environment

## Getting started

### Vagrant

1. Install VirtualBox and Vagrant
    ```sh
    brew install virtualbox vagrant
    ```
1. Clone this repo into a folder
1. Start up the server with Vagrant and ssh into it:
    ```sh
    vagrant up
    ```

### Ansible

Ansible is used to provision your Ubuntu box, so please ensure that Ansible is installed on your host machine.

#### Python

I would recommend installing Python3 via brew, so that you are not using macOS's built-in version.

```sh
brew install python  # python3 seems to have been rename to python in brew now 
```

#### Install Ansible

```sh
sudo pip3 install ansible

# or to update ansible
sudo pip3 install ansible --upgrade
```

#### Ansible dependencies

Ansible uses WinRM to communicate with the Ubuntu Box, so you will need to install the Python WinRM library

```sh
pip3 install pywinrm
```

## Notes