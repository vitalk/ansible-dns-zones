DNS Zones
=========

Ansible role to generate dns zones from jinja templates.

Role Variables
--------------

Option | Description
--- | ---
`dns_zones` | An optional list of dns zones to generate. You **must select** zones you want to generate explicitly.
`dns_zones_input_directory` | Path to zone files templates. Defaults to `templates` in the role directory.
`dns_zones_output_directory` | The destination directory for generated zones. Defaults to `files` in the role directory.

Usage Example
-------------

Explicitly define template for each zone you wanna to create...

```jinja
# file: templates/db.example.com.j2
{% extends 'db.zone.j2' %}
{% set serial = 2014080301 %}

{% block a %}
            IN  A       1.2.3.4
ns1         IN  A       1.2.3.4
mail        IN  A       1.2.3.4
www         IN  CNAME   @
{% endblock %}
```

```yaml
# file: test.yml
---
- hosts: all
  gather_facts: no
  vars:
    dns_zones:
      - name: example.com
  roles:
    - .
```

And finally play it...

```bash
ansible-playbook -i hosts.example test.yml
```

License
-------

Licensed under the [MIT license](http://mit-license.org/vitalk).

Self-Promotion
--------------

Created by Vital Kudzelka.

Don't hesitate create [a GitHub Issue](https://github.com/vitalk/ansible-dns-zones/issues) if you have any suggestions or found a bug.
