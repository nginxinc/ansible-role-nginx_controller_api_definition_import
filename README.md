NGINX Controller Certificate
============================

Upsert (create and update) certificates to NGINX Controller for use with Gateways and Components.

Requirements
------------

[NGINX Controller](https://www.nginx.com/products/nginx-controller/)

Role Variables
--------------

### Required Variables

`nginx_controller.fqdn` - The hostname or DNS of the NGINX Controller instance.

`nginx_controller.auth_token` - An authentication token for the NGINX Controller API (the nginx_controller_generate_token role outputs this).

`nginx_controller_api_specification_import_file`

`nginx_controller_api_specification_version`

`nginx_controller_api_specification_name`

### Template Variables

This role has multiple template related variables. The descriptions and defaults for all these variables can be found in **[vars/main.yml](./vars/main.yml)**

Dependencies
------------

Example Playbook
----------------

To use this role you can create a playbook such as the following (let's name it `nginx_controller_certificate.yaml` for the purposes of this example).

```yaml
- hosts: localhost
  gather_facts: no
  vars:
    nginx_controller_user_email: "user@example.com"
    nginx_controller_user_password: "mySecurePassword"
    nginx_controller_fqdn: "controller.mydomain.com"
    nginx_controller_validate_certs: false

  tasks:
    - name: Retrieve the NGINX Controller auth token
      include_role:
        name: nginxinc.nginx_controller_generate_token

    - name: Import the API specification
      include_role:
        name: nginxinc.nginx_controller_api_import
      vars:
        nginx_controller_api_specification_version:
        nginx_controller_api_specification_body_format:
        nginx_controller_api_specification_name:
        nginx_controller_api_specification:
```

You can then run `ansible-playbook nginx_controller_api_specification_import.yaml` to execute the playbook.

Alternatively, you can also pass/override any variables at run time using the `--extra-vars` or `-e` flag like so `ansible-playbook nginx_controller_api_specification_import.yaml -e "nginx_controller_user_email=user@company.com nginx_controller_user_password=notsecure nginx_controller_fqdn=controller.example.local nginx_controller_validate_certs=false"`

You can also pass/override any variables by passing a `yaml` file containing any number of variables like so `ansible-playbook nginx_controller_api_specification_import.yaml -e "@nginx_controller_api_specification_import_vars.yaml"`

License
-------

[Apache License, Version 2.0](./LICENSE)

Author Information
------------------

[Brian Ehlert](https://github.com/brianehlert)

&copy; [NGINX, Inc.](https://www.nginx.com/) 2020
