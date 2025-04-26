# Ansible Playbooks in /test Directory

This directory contains various Ansible playbooks for testing and demonstration purposes.

## Files

*   **`ansible_starting_vm_script_in_proxmox.yaml`**: Schedules the creation of snapshots for all VMs listed in a Proxmox node via cron. It dynamically generates individual snapshot playbooks for each VM. *(Note: The filename is slightly misleading; it deals with snapshot scheduling, not starting VMs)*.
*   **`create_vlan.yaml`**: Creates a new VLAN on a specified bridge within a Proxmox environment using the Proxmox API.
*   **`install_apache.yaml`**: Manages web servers on specific hosts: uninstalls Apache on `ubuntu1`, installs Nginx on `ubuntu2`, and attempts to start both services.
*   **`inventory.yaml`**: Defines the inventory of managed hosts, including groups (`ubuntu`, `proxmox`) and connection variables (IP addresses, users, SSH keys, passwords).
*   **`playbook-update.yaml`**: Updates the package cache and upgrades all packages (`dist-upgrade`) on Debian/Ubuntu-based systems. It also checks if a reboot is required due to kernel updates and performs one if necessary.
*   **`shutdown_all_servers.yaml`**: (Contents not provided) Presumably, this playbook is designed to shut down servers listed in the inventory.
*   **`use_variable_in_ansible.yaml`**: Demonstrates how to install a list of packages defined in a variable (`packages_to_install`) using the `ansible.builtin.apt` module.
