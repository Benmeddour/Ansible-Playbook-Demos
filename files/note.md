# Static Files in Ansible Roles  

When organizing static files in an Ansible role, place them under a dedicated `files/` directory within the role. This enables modules like `copy` and `unarchive` to manage these assets seamlessly.  

Example Role Layout:  
```text
roles/
└── base/
    ├── files/
    │   └── test_site.html
    └── tasks/
        └── main.yaml
```  

Usage Example:  
```yaml
- name: Copy static HTML file to remote server
  ansible.builtin.copy:
    src: test_site.html
    dest: /var/www/html/test_site.html
```  

Best Practices:  
- Keep file paths relative to the role's `files/` directory.  
- Use the `templates/` directory for Jinja2 template files.  
- Choose clear, descriptive filenames to avoid collisions.  
- Consult the official docs for more on role reuse: https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html#role-file-variable-precedence  

