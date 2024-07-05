Deploy Echo Service with Ansible

This project provides an Ansible playbook to deploy a simple Echo Service on a Debian virtual machine. The Echo Service is implemented using Flask and runs as a systemd service.
Prerequisites

    Ansible installed on your local machine.
    Access to a Debian virtual machine (VM).
    SSH access to the VM.
    OpenStack client configured (if using OpenStack to manage your VM).

Inventory Setup

Create an inventory file named hosts.ini with the details of your Debian VM:
[debian_vms]
debian-vm ansible_host=<your-vm-ip> ansible_user=<your-ssh-user>
Replace <your-vm-ip> with the IP address of your VM and <your-ssh-user> with the username you use to SSH into the VM (usually debian or root).

Playbook Description

The Ansible playbook echo_service.yml will perform the following tasks:

    Update the APT package repository cache.
    Install Python3, pip, and venv.
    Create a directory for the echo service.
    Create a Python virtual environment.
    Install Flask in the virtual environment.
    Create the echo service script.
    Create a systemd service file for the echo service.
    Reload systemd to recognize the new service.
    Start and enable the echo service.

Playbook
Create a file named echo_service.yml with the mentioned content.

Running the Playbook

Execute the playbook with Ansible:
ansible-playbook -i hosts.ini echo_service.yml

Verifying the Deployment

Once the playbook has run successfully, the echo service should be running on your Debian VM. You can verify it by making a GET request to the service:

curl http://<your-vm-ip>:5000/?message=Hello

You should receive a JSON response with your message:

json

{
  "message": "Hello"
}
