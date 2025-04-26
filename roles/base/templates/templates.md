# Ansible Templates

Ansible templates allow you to create dynamic configuration files based on variables. They leverage the Jinja2 templating engine, a powerful Python library for generating text-based formats (HTML, XML, CSV, configuration files, etc.).

## Benefits of Using Templates

*   **Dynamic Configuration:** Generate configuration files tailored to specific hosts or environments using variables.
*   **Consistency:** Ensure configuration files are consistent across multiple servers, reducing errors caused by manual edits.
*   **Reusability:** Create a single template file that can be used for various scenarios by changing the input variables.
*   **Separation of Concerns:** Keep configuration logic separate from the actual configuration file structure, making playbooks cleaner and easier to maintain.
*   **Reduced Complexity:** Manage complex configurations with conditional logic, loops, and filters within the template itself.

## Explanation

Ansible's `template` module transfers a file from the control node to the target node(s). Before transferring, it processes the file through the Jinja2 templating engine. Any Jinja2 expressions or variables within the template file (usually ending with a `.j2` extension) are evaluated and replaced with their corresponding values.

Key Jinja2 syntax used in Ansible templates:

*   `{{ variable_name }}`: Used to substitute the value of an Ansible variable.
*   `{% if condition %}` ... `{% else %}` ... `{% endif %}`: Conditional statements.
*   `{% for item in list %}` ... `{% endfor %}`: Loops.

## Example

Let's create a simple Nginx configuration file using an Ansible template.

**1. Define Variables (e.g., in `vars/main.yml` or playbook vars):**

```yaml
nginx_port: 8080
server_name: myapp.example.com
doc_root: /var/www/myapp
```

**2. Create the Template File (`templates/nginx.conf.j2`):**

```nginx
server {
    listen {{ nginx_port }};
    server_name {{ server_name }};

    root {{ doc_root }};
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }

    # Add more configurations as needed
}
```

**3. Use the `template` Module in Your Playbook:**

```yaml
---
- name: Configure Nginx using a template
  hosts: ubuntu
  vars:
    nginx_port: 8080
    server_name: myapp.example.com
    doc_root: /var/www/myapp
  tasks:
    - name: Ensure Nginx package is present
      ansible.builtin.package:
        name: nginx
        state: present

    - name: Deploy Nginx configuration from template
      ansible.builtin.template:
        src: nginx.conf.j2  # Path to the template file on the control node
        dest: /etc/nginx/conf.d/myapp.conf # Path on the target node
        owner: root
        group: root
        mode: '0644'
      notify: Restart Nginx # Handler to restart Nginx after config change

  handlers:
    - name: Restart Nginx
      ansible.builtin.service:
        name: nginx
        state: restarted
```

**4. Resulting File (`/etc/nginx/conf.d/myapp.conf` on the target host):**

After running the playbook, the `myapp.conf` file on the target `webservers` will look like this:

```nginx
server {
    listen 8080;
    server_name myapp.example.com;

    root /var/www/myapp;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }

    # Add more configurations as needed
}
```

This example demonstrates how variables defined in the playbook are used to dynamically generate the Nginx configuration file from the `nginx.conf.j2` template.

for more about ansible `template module`, check the official documentation: [**ansible.builtin.template module – Template a file out to a target host**](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/template_module.html)