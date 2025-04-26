# Recommended Ansible Project Layout  

This document provides a clear, scalable directory structure tailored for Ansible projects. It helps you maintain separation of concerns, reuse roles, and organize inventories and playbooks for multiple environments.  

Key Sections:  
- `ansible.cfg` sets project-wide configuration.  
- `inventory/` holds environment-specific host definitions and variable files.  
- `roles/` groups reusable logic into named roles with tasks, handlers, files, templates, and metadata.  
- `playbooks/` contains top‑level playbook files that orchestrate roles.  
- `files/` and `templates/` at project root for shared static assets and Jinja2 templates.  

Best Practices:  
- Version control your entire project directory, including inventories and roles.  
- Keep environment inventories (e.g., staging, production) isolated.  
- Use `group_vars/` and `host_vars/` for fine‑grained variable management.  
- Leverage `meta/main.yml` in roles for dependencies and supported platforms.  
- Document each role’s purpose in its `README.md`.  
- Pin Ansible version in `ansible.cfg` to avoid compatibility issues.  

Further Reading:  
- Official Ansible Best Practices Guide: https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html  

##  Best Practice: Project Directory Structure  

```text
├── ansible.cfg          # Ansible configuration file
├── inventory/
│   ├── production       # Production inventory file
│   ├── staging          # Staging inventory file
│   ├── group_vars/
│   │   ├── all.yml          # Variables for all groups
│   │   ├── webservers.yml   # Variables for the 'webservers' group
│   │   └── dbservers.yml    # Variables for the 'dbservers' group
│   └── host_vars/
│       ├── server1.example.com.yml # Variables specific to server1
│       └── server2.example.com.yml # Variables specific to server2
├── roles/
│   ├── common/          # Common role applied to all hosts
│   │   ├── tasks/
│   │   │   └── main.yml
│   │   ├── handlers/
│   │   │   └── main.yml
│   │   ├── templates/
│   │   ├── files/
│   │   ├── vars/
│   │   │   └── main.yml
│   │   └── meta/
│   │       └── main.yml
│   ├── webserver/       # Role for webservers
│   │   └── ... (similar structure as 'common')
│   └── dbserver/        # Role for database servers
│       └── ... (similar structure as 'common')
├── playbooks/
│   ├── site.yml         # Main playbook applying roles to hosts
│   ├── webservers.yml   # Playbook specific to webservers
│   └── dbservers.yml    # Playbook specific to dbservers
└── files/               # Static files copied to hosts
└── templates/           # Jinja2 templates
```

