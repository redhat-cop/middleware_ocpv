[![CI](https://github.com/redhat-cop/middleware_ocpv/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/redhat-cop/middleware_ocpv/actions/workflows/ci.yml) [![OpenSSF Best Practices](https://www.bestpractices.dev/projects/8292/badge)](https://www.bestpractices.dev/en/projects/8292)

# Middleware Ansible Middleware OpenShift Virtualization collection

Using OpenShift Virtualization as an environment for hosting Virtual Machines that are provisioned, configured and maintained using Ansible and tooling from the Ansible Middleware project.

## Use case of middleware_ocpv collection

The `middleware_ocpv` collection in infrastructure automation leverages Ansible to seamlessly handle the complete lifecycle of Virtual Machines within an OpenShift Virtualization runtime environment. It extends its functionality beyond VM management to include the streamlined installation, configuration, and ongoing management of deployed instances using the JBoss Enterprise Application Server (EAP).

What sets the `middleware_ocpv` collection apart is its ability to bridge the gap between the intricacies of OpenShift Virtualization and the demands of JBoss EAP deployments. Ansible serves as the linchpin, providing a user-friendly and cohesive platform for administrators to navigate the complexities of managing VMs and ensuring the seamless operation of enterprise-level applications.

This integration highlights the adaptability of Ansible in managing Virtual Machines within the dynamic and scalable OpenShift Virtualization environment, treating them with the same ease as any other hosting environment. Furthermore, by showcasing the deployment and management of an entire fleet of instances running Red Hat Application Services, the power and simplicity of Ansible automation become evident. The `middleware_ocpv` collection thus serves as a robust solution for efficiently handling diverse workloads in a sophisticated and integrated manner.

## Environment Requirements

For this collection, the following resources must be available:

* OpenShift Container Platform
    * Capable of running OpenShift Virtualization ([Requirements](https://docs.openshift.com/container-platform/4.12/virt/install/preparing-cluster-for-virt.html#virt-hardware-os-requirements_preparing-cluster-for-virt))
    * `cluster-admin` access
* Ansible Controller (Part of Ansible Automation Platform) deployed to the same OpenShift environment as OpenShift Virtualization.
* Control Node capable of provisioning the collection environment
    * Ansible

## Prerequisites

Certain requirements must be met prior to realizing the full potential of this collection. This involves not only completing steps within a local machine (control host), but also obtaining assets from external systems.

### Clone the Repository

Tooling is available within this repository to provision the collection. Clone the repository to your local machine:

```shell
git clone https://github.com/redhat-cop/middleware_ocpv.git
cd middleware_ocpv
```

### SSH Keypair

An SSH keypair is needed to communicate with the provisioned virtual machine. Provide the location of an SSH (without password) public key (`.pub`) and private key within the `ssh_public_key_path` and `ssh_private_key_path` variables in the [vars/provision.yml](vars/provision.yml) file.

### Automation Hub Token

A token for the public Automation Hub must be obtained so that it can be configured to access certified content locally as part of the setup and provisioning process as well as being stored in Ansible Controller. 

Steps for obtaining the token can be found [here](https://cloud.redhat.com/ansible/automation-hub/token/)

The token must be added to two (2) locations:

1. Set the value of `token` in the [ansible.cfg](ansible.cfg) file
2. Set the value of the `automationhub_token` variables in the [vars/provision.yml](vars/provision.yml) file

### Red Hat Service Account

A Service Account as the associated Client ID and Client Secret must be provided so that the middleware assets can be generated from the Red Hat Customer Portal.

Obtain a Client ID and Client Secret by generating a Service Account [here](https://console.redhat.com/application-services/service-accounts).

Set the values of the `jbossnetwork_client_id` and `jbossnetwork_client_secret` variables in the [vars/provision.yml](vars/provision.yml) file.

### Red Hat Customer Portal Account

The provisioned Virtual Machine will be subscribed so that it can obtain the required packages. Populate the `redhat_csp_username` and `redhat_csp_password` variables in the [vars/provision.yml](vars/provision.yml) file with these values.

### Ansible Controller

The provisioning process will configure Ansible Controller to manage the collection. The location of Controller as well as credentials must be specified. Set the `controller_hostname`, `controller_username` and `controller_password` variables in the [vars/provision.yml](vars/provision.yml) file.

### Python Dependencies

Install the required Python dependencies by executing the following command from the root of the cloned repository:

```shell
pip install -r requirements.txt
```

### Ansible Dependencies

Install the required Ansible dependencies by executing the following command from the root of the cloned repository:

```shell
ansible-galaxy collection install -r requirements.yml
```

## Provision the collection

Provisioning the collection performs the following actions:

* Configures Ansible Controller
    * Custom Credential Types
    * Credentials
    * Organization
    * Project
    * Inventory
    * Job Templates
        * Deploy OCPv
        * Deploy collection

Ensure that you are logged into the OpenShift environment with a user with `cluster-admin` permissions and execute the following command:

```shell
ansible-playbook playbooks/provision.yml
```

## Executing the collection

Once the configuration of Ansible Controller has completed successfully, login to Ansible Controller and navigate to the **Templates** tab underneath _Resources_.

Deploy OpenShift Virtualization by selecting the rocketship next to the _Deploy OCPv_ Job Template to install and configure OpenShift Virtualization.

Once OpenShift Virtualization has been installed, execute the collection playbook. The collection provisioning process will perform the following actions:

1. Create a new OpenShift namespace called `ansible-middleware-ocpv`.
2. Create a RHEL 9 based Virtual Machine
3. Perform Dynamic discovery of VirtualMachine instance to populate an inventory group called `eap` within the `ocpv` inventory.
4. Configure the Virtual Machine with the following:
    1. JBoss Enterprise Application Platform 7.4.0 (and associated dependencies [OpenJDK])
    2. Systemd service for JBoss EAP
    3. Deploy a sample application and make it available at the `/info` context
5. Create an OpenShift _Service_ and _Route_ exposing the JBoss Server

Once the automation has completed successfully, navigate to the `ansible-middleware-ocpv` within the OpenShift web console.

Within Administrator perspective, expand the _Networking_ navigation pane on the left-hand side and select **Routes**. 

Select the **eap-collection** route which will open the exposed VM and present the JBoss EAP welcome page.

Navigate to the `/info` context to view the deployed application.

Enjoy seeing the power of Ansible Middleware setup, configure and automate the deployment of Red Hat middleware within the OpenShift Container Platform!

# License

[Apache License Version 2.0](https://github.com/redhat-cop/middleware_ocpv/blob/main/LICENSE)