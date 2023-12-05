Jupyter
=======

[JupyterHub](https://jupyter.org/hub) role for SURF Research Cloud. Adapted from the [eWaterCycle lab infrastructure](https://github.com/eWaterCycle/infra).

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

```yaml
cull:
  # Servers and notebooks that have been idle for longer then timeout (in seconds) will be culled.
  timeout: '86400' # 1 day
  # The maximum age (in seconds) of servers that should be culled even if they are active.
  max_age: '604800' # 7 days
```

Dependencies
------------

The Jupyter Hub requires python packages which can be installed using `pip`, see the [python role](../python).

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

Apache-2.0

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
