deploy_collection
=========

Deployment of the core components of the Ansible Middleware OpenShift Virtualization collection

Role Variables
--------------

| Variable                              | Description                            | Default                                           |
|:--------------------------------------|:---------------------------------------|:--------------------------------------------------|
| `collection_namespace`                | `namspace of collection`               | `ansible-middleware-ocpv`                         |
| `collection_name`                     | `deployed collection name`             | `eap-collection`                                  |
| `vm_cpus_cores`                       | `VM CPU core counts`                   | `2`                                               |                                                       
| `vm_cpus_sockets`                     | `VM CPU socket counts`                 | `1`                                               |
| `vm_cpus_threads`                     | `VM CPU thread counts`                 | `1`                                               |                                                     
| `vm_machine_type`                     | `VM machine type`                      | `pc-q35-rhel8.4.0`                                |                                      
| `vm_storage_requests`                 | `VM storage space`                     | `50Gi`                                            |                                              
| `vm_memory_requests`                  | `VM memory requests`                   | `8Gi`                                             |                                                
| `vm_datasource_name`                  | `VM datasource name`                   | `rhel9`                                           |
| `vm_datasource_namespace`             | `VM datasource namespace`              | `openshift-virtualization-os-images`              |
| `deploy_collection_vm_ssh_public_key` | `VM SSH publick key`                   | `You need to provide your vm ssh pubkey`          | 
| `cloud_init_secret`                   | `cloud inti secret`                    | `cloud-init`                                      |
| `eap_product_version`                 | `EAP version`                          | `7.4`                                             |
| `eap_version`                         | `specific EAP version including minor` | `7.4.0`                                           |                                                     
| `eap_product_category`                | `EAP product category`                 | `appplatform`                                     |                                       
| `eap_product_type`                    | `EAP product type`                     | `DISTRIBUTION`                                    |                                          
| `eap_product_filename`                | `EAP filename`                         | `jboss-eap-7.4.0.zip$`                            |                            
| `eap_java_package_name`               | `Needed Java package name for EAP`     | `java-11-openjdk-headless.x86_64`                 |                  
| `eap_archive_dir`                     | `EAP archive directory`                | `/tmp/eap_archive/`                               |                                      
| `eap_archive_filename`                | `EAP archive filename`                 | `jboss-eap-{{ eap_version }}.zip`                 |                 
| `eap_download_location`               | `EAP download location in machine`     | `{{ eap_archive_dir }}{{ eap_archive_filename }}` |
| `eap_bind_addr`                       | `EAP bind address`                     | `0.0.0.0`                                         |                                                

Dependencies
------------

* [kubernetes.core](https://docs.ansible.com/ansible/latest/collections/kubernetes/core/index.html)
* [ansible.controller](https://docs.ansible.com/automation.html)
* [infra.controller_configuration](https://galaxy.ansible.com/infra)

Example Playbook
----------------

Please
follow [deploy_collection.yml](https://github.com/redhat-cop/middleware_ocpv/blob/main/playbooks/deploy_collection.yml)
for
better understanding.

License
-------

[Apache License Version 2.0](https://github.com/redhat-cop/middleware_ocpv/blob/main/LICENSE)

Author Information
------------------

- [Andrew Block](https://github.com/sabre1041)
- [Guido Grazioli](https://github.com/guidograzioli)
- [Ranabir Chakraborty](https://github.com/RanabirChakraborty)
