ocpv_install
=========

Deployment of OpenShift Virtualization to an OpenShift environment

Role Variables
--------------

| Variable                               | Description                               | Default                   |
|:---------------------------------------|:------------------------------------------|:--------------------------|
| `ocpv_operator_name`                   | `OCPV operator name`                      | `kubevirt-hyperconverged` |
| `ocpv_namespace`                       | `OCPV namespace`                          | `openshift-cnv`           |
| `ocpv_automatic_install_plan_approval` | `automatic install plan approval of OCPV` | `true`                    |
| `ocpv_operator_catalog`                | `OCPV operator catalog`                   | `redhat-operators`        |
| `ocpv_starting_csv`                    | `OCPV starting csv`                       |                           |
| `ocpv_channel`                         | `OCPV channel name`                       |                           |
| `ocpv_csv_ignore_error`                | `OCPV csv ignore error boolean value`     | `false`                   |

Dependencies
------------

* [kubernetes.core](https://docs.ansible.com/ansible/latest/collections/kubernetes/core/index.html)
* [ansible.controller](https://docs.ansible.com/automation.html)
* [infra.controller_configuration](https://galaxy.ansible.com/infra)

Example Playbook
----------------

Please follow [install_ocpv.yml](https://github.com/redhat-cop/middleware_ocpv/blob/main/playbooks/install_ocpv.yml)
for better understanding.

License
-------

[Apache License Version 2.0](https://github.com/redhat-cop/middleware_ocpv/blob/main/LICENSE)

Author Information
------------------

- [Andrew Block](https://github.com/sabre1041)
- [Guido Grazioli](https://github.com/guidograzioli)
- [Ranabir Chakraborty](https://github.com/RanabirChakraborty)
