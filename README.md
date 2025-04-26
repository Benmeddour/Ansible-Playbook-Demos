# Ansible Playbook Demonstrations (Test Project)

This repository contains a collection of Ansible playbooks, configuration files, and roles designed for testing, learning, and demonstrating various infrastructure automation tasks.

## Prerequisites

*   **Ansible:** Ensure Ansible is installed on your control node. Refer to the [official Ansible installation guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html).
*   **Target Hosts:** You need accessible target machines (like VMs or physical servers) configured in the inventory file (`inventory.yaml`) with appropriate SSH access and potentially Python installed.

## Repository Structure Overview

This project follows a standard Ansible project structure:

*   `ansible.cfg`: Project-specific Ansible configuration (e.g., inventory path, roles path).
*   `inventory.yaml`: Defines managed hosts, groups, and connection details.
*   `group_vars/`: Contains variable files applied to specific host groups (e.g., `ubuntu.yaml`, `proxmox.yaml`).
*   `host_vars/`: Contains variable files applied to specific hosts (e.g., `ubuntu1.yaml`, `proxmox1.yaml`).
*   `files/`: Stores static files to be copied to managed nodes (e.g., configuration files, scripts).
*   `roles/`: Contains reusable Ansible roles for modular automation. See the "Roles" section below for details.
*   `*.yaml`: Top-level playbook files orchestrating tasks. See the "Playbooks" section below.
*   `best_structre_for_ansible/`: Contains documentation (`best_structure_for_ansible.md`) outlining recommended practices for structuring Ansible projects.
*   `LICENSE`: The license under which this project is distributed (Apache License 2.0).
*   `.gitignore`: Specifies files and directories ignored by Git.

## Playbooks

These YAML files define the automation tasks to be executed:

*   `bootstrap.yaml`: Performs initial setup on control and target nodes.
*   `roles.yaml`: Applies a collection of roles defined within the `roles/` directory to target hosts. *Consider renaming this to `site.yaml` or similar for convention.*
*   `install_apache.yaml`: Manages web server installations (e.g., installs Nginx, potentially removes Apache).
*   `managing_file_service.yaml`: Demonstrates deploying files and managing system services.
*   `managing_users.yaml`: Manages user accounts and their permissions on target systems.
*   `playbook-update.yaml`: Updates system packages and handles reboots if necessary.
*   `shutdown_all_servers.yaml`: Gracefully shuts down all servers listed in the inventory.
*   `use_variable_in_ansible.yaml`: Installs a list of packages defined in variables.
*   `host_group_vars.yaml`: *Likely an example playbook demonstrating variable precedence, potentially misplaced.*
*   `proxmox/create_new_user_proxmox.yaml`: Creates new user accounts within Proxmox.

## Roles

Reusable units of automation:

*   `roles/admin_ubt`: Tasks, handlers, and variables for common administrative actions on Ubuntu systems.
*   `roles/base`: Foundational configuration applied to most hosts (tasks and templates).
*   `roles/base/templates/templates.md`: Guide explaining the use of Jinja2 templates in Ansible, including benefits, syntax, and an example (e.g., Nginx configuration).
*   `roles/root_proxmox`: Tasks specific to root-level operations on Proxmox hosts.
*   `roles/test_hendlers`: A role likely designed to test Ansible handler functionality.

## Usage

1.  **Clone the repository** (if you haven't already): `git clone https://github.com/Benmeddour/Ansible-Playbook-Demos.git`
2.  **Navigate** into the cloned project directory: `cd Ansible-Playbook-Demos/`
3.  **Review and customize** the inventory (`inventory.yaml`) and variable files (`group_vars/`, `host_vars/`) for your environment.
4.  **Run a playbook** using the `ansible-playbook` command. Use the `-i` flag if your inventory file isn't named `inventory.yaml` or specified in `ansible.cfg`.

    ```bash
    # Example: Run the package update playbook
    ansible-playbook playbook-update.yaml

    # Example: Run the playbook to apply roles
    ansible-playbook roles.yaml

    # Example: Run a playbook targeting only the 'ubuntu' group
    ansible-playbook install_apache.yaml --limit ubuntu
    ```

## Detailed Directory Structure

```text
├── best_structre_for_ansible/          # Folder containing documentation on best practices
│   └── best_structure_for_ansible.md   # Markdown file detailing recommended Ansible structure
├── files/                              # Directory for static files to be copied to managed nodes
│   ├── note.md                         # A note file
│   ├── sudoers_ansible                 # Configuration file for sudoers, managed by Ansible
│   └── test_site.html                  # HTML file for a test website
├── group_vars/                         # Directory containing variables for specific host groups
│   ├── proxmox.yaml                    # Variables specific to the 'proxmox' group
│   └── ubuntu.yaml                     # Variables specific to the 'ubuntu' group
├── host_vars/                          # Directory containing variables for specific hosts
│   ├── proxmox1.yaml                   # Variables specific to the host 'proxmox1'
│   ├── ubuntu1.yaml                    # Variables specific to the host 'ubuntu1'
│   └── ubuntu2.yaml                    # Variables specific to the host 'ubuntu2'
├── proxmox/                            # Directory related to Proxmox specific tasks/playbooks
│   └── create_new_user_proxmox.yaml    # Playbook for creating a new user in Proxmox
├── roles/                              # Directory containing reusable Ansible roles
│   ├── admin_ubt/                      # Role for administrative tasks on Ubuntu
│   │   ├── handlers/                   # Handlers for the 'admin_ubt' role
│   │   │   └── main.yaml               # Main handlers file
│   │   ├── tasks/                      # Tasks for the 'admin_ubt' role
│   │   │   └── main.yaml               # Main tasks file
│   │   └── vars/                       # Variables for the 'admin_ubt' role
│   │       └── main.yaml               # Main variables file
│   ├── base/                           # A base role, likely applied to many hosts
│   │   ├── tasks/                      # Tasks for the 'base' role
│   │   │   └── main.yaml               # Main tasks file
│   │   └── templates/                  # Templates for the 'base' role
│   │       └── templates.md            # Markdown file related to templates (likely documentation or example)
│   ├── root_proxmox/                   # Role related to root tasks on Proxmox
│   │   └── tasks/                      # Tasks for the 'root_proxmox' role
│   │       └── main.yaml               # Main tasks file
│   └── test_hendlers/                  # Role likely for testing handlers
│       ├── handlers/                   # Handlers for the 'test_hendlers' role
│       │   └── main.yaml               # Main handlers file
│       └── tasks/                      # Tasks for the 'test_hendlers' role
│           └── main.yaml               # Main tasks file
├── .gitignore                          # Specifies intentionally untracked files that Git should ignore
├── LICENSE                             # Project license file
├── README.md                           # Project overview and documentation (this file)
├── ansible.cfg                         # Ansible configuration file for the project
├── bootstrap.yaml                      # Playbook for initial server setup/bootstrapping
├── host_group_vars.yaml                # Playbook likely demonstrating host/group variable usage (potentially misplaced)
├── install_apache.yaml                 # Playbook for installing Apache web server
├── inventory.yaml                      # Main inventory file defining hosts and groups
├── managing_file_service.yaml          # Playbook for managing file services
├── managing_users.yaml                 # Playbook for managing user accounts
├── playbook-update.yaml                # Playbook for updating systems or applications
├── roles.yaml                          # Playbook likely for applying roles (could be named better, e.g., site.yaml)
├── shutdown_all_servers.yaml           # Playbook for shutting down servers
└── use_variable_in_ansible.yaml        # Playbook demonstrating variable usage in Ansible
```

## License

This project is licensed under the Apache License 2.0. See the [LICENSE](LICENSE) file for details.