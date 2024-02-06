# kubeone

[![Source Code](https://img.shields.io/badge/github-source%20code-blue?logo=github&logoColor=white)](https://github.com/rolehippie/kubeone)
[![General Workflow](https://github.com/rolehippie/kubeone/actions/workflows/general.yml/badge.svg)](https://github.com/rolehippie/kubeone/actions/workflows/general.yml)
[![Readme Workflow](https://github.com/rolehippie/kubeone/actions/workflows/docs.yml/badge.svg)](https://github.com/rolehippie/kubeone/actions/workflows/docs.yml)
[![Galaxy Workflow](https://github.com/rolehippie/kubeone/actions/workflows/galaxy.yml/badge.svg)](https://github.com/rolehippie/kubeone/actions/workflows/galaxy.yml)
[![License: Apache-2.0](https://img.shields.io/github/license/rolehippie/kubeone)](https://github.com/rolehippie/kubeone/blob/master/LICENSE)
[![Ansible Role](https://img.shields.io/badge/role-rolehippie.kubeone-blue)](https://galaxy.ansible.com/rolehippie/kubeone)

Ansible role to install KubeOne and bootstrap Kubernetes.

## Sponsor

Building and improving this Ansible role have been sponsored by my current and previous employers like **[Cloudpunks GmbH](https://cloudpunks.de)** and **[Proact Deutschland GmbH](https://www.proact.eu)**.

## Table of content

- [Requirements](#requirements)
- [Default Variables](#default-variables)
  - [kubeone_addons_enable](#kubeone_addons_enable)
  - [kubeone_addons_extra](#kubeone_addons_extra)
  - [kubeone_addons_general](#kubeone_addons_general)
  - [kubeone_addons_path](#kubeone_addons_path)
  - [kubeone_apiserver_host](#kubeone_apiserver_host)
  - [kubeone_apiserver_port](#kubeone_apiserver_port)
  - [kubeone_apiserver_sans](#kubeone_apiserver_sans)
  - [kubeone_cloud_provider](#kubeone_cloud_provider)
  - [kubeone_cluster_name](#kubeone_cluster_name)
  - [kubeone_cni_config](#kubeone_cni_config)
  - [kubeone_cni_provider](#kubeone_cni_provider)
  - [kubeone_config_content](#kubeone_config_content)
  - [kubeone_config_path](#kubeone_config_path)
  - [kubeone_configure_repositories](#kubeone_configure_repositories)
  - [kubeone_control_plane](#kubeone_control_plane)
  - [kubeone_domain_name](#kubeone_domain_name)
  - [kubeone_dynamic_auditlog_enable](#kubeone_dynamic_auditlog_enable)
  - [kubeone_dynamic_workers](#kubeone_dynamic_workers)
  - [kubeone_encryption_providers_config](#kubeone_encryption_providers_config)
  - [kubeone_encryption_providers_enable](#kubeone_encryption_providers_enable)
  - [kubeone_environment_variables](#kubeone_environment_variables)
  - [kubeone_force_apply](#kubeone_force_apply)
  - [kubeone_force_install](#kubeone_force_install)
  - [kubeone_force_upgrade](#kubeone_force_upgrade)
  - [kubeone_install_path](#kubeone_install_path)
  - [kubeone_kubernetes_version](#kubeone_kubernetes_version)
  - [kubeone_log_path](#kubeone_log_path)
  - [kubeone_machine_controller](#kubeone_machine_controller)
  - [kubeone_manifest_version](#kubeone_manifest_version)
  - [kubeone_metrics_server_enable](#kubeone_metrics_server_enable)
  - [kubeone_node_ports](#kubeone_node_ports)
  - [kubeone_openid_connect_config](#kubeone_openid_connect_config)
  - [kubeone_openid_connect_enable](#kubeone_openid_connect_enable)
  - [kubeone_pod_node_selector_config](#kubeone_pod_node_selector_config)
  - [kubeone_pod_node_selector_enable](#kubeone_pod_node_selector_enable)
  - [kubeone_pod_subnet](#kubeone_pod_subnet)
  - [kubeone_release_download](#kubeone_release_download)
  - [kubeone_release_version](#kubeone_release_version)
  - [kubeone_rotate_encryption_key](#kubeone_rotate_encryption_key)
  - [kubeone_service_subnet](#kubeone_service_subnet)
  - [kubeone_static_auditlog_config](#kubeone_static_auditlog_config)
  - [kubeone_static_auditlog_enable](#kubeone_static_auditlog_enable)
  - [kubeone_static_workers](#kubeone_static_workers)
  - [kubeone_upgrade_machine_deployments](#kubeone_upgrade_machine_deployments)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Requirements

- Minimum Ansible version: `2.10`

## Default Variables

### kubeone_addons_enable

Enable addons

#### Default value

```YAML
kubeone_addons_enable: true
```

### kubeone_addons_extra

Extra list of addons to enable

#### Default value

```YAML
kubeone_addons_extra: []
```

#### Example usage

```YAML
kubeone_addons_extra:
  - name: backup-restic
    url: https://github.com/kubermatic/kubeone/raw/master/addons/backups-restic/backups-restic.yaml
    params:
      resticPassword: p455w0rd
  - name: unattended-upgrades
    ansible.builtin.file: apt.yml
    url: https://github.com/kubermatic/kubeone/raw/master/addons/unattended-upgrades/apt.yaml
  - name: unattended-upgrades
    ansible.builtin.file: yum.yml
    url: https://github.com/kubermatic/kubeone/raw/master/addons/unattended-upgrades/yum.yaml
  - name: dummy1
    content: |
      apiVersion: apps/v1
      kind: DaemonSet
      ...
    params:
      param1: value1
      param2: value2
      param3: value3
    delete: True
  - name: dummy1
    state: absent
```

### kubeone_addons_general

General list of addons to enable

#### Default value

```YAML
kubeone_addons_general: []
```

#### Example usage

```YAML
kubeone_addons_general:
  - name: backup-restic
    url: https://github.com/kubermatic/kubeone/raw/master/addons/backups-restic/backups-restic.yaml
    params:
      resticPassword: p455w0rd
  - name: unattended-upgrades
    ansible.builtin.file: apt.yml
    url: https://github.com/kubermatic/kubeone/raw/master/addons/unattended-upgrades/apt.yaml
  - name: unattended-upgrades
    ansible.builtin.file: yum.yml
    url: https://github.com/kubermatic/kubeone/raw/master/addons/unattended-upgrades/yum.yaml
  - name: dummy1
    content: |
      apiVersion: apps/v1
      kind: DaemonSet
      ...
    params:
      param1: value1
      param2: value2
      param3: value3
    delete: True
  - name: dummy1
    state: absent
```

### kubeone_addons_path

Path to installed addons

#### Default value

```YAML
kubeone_addons_path: '{{ kubeone_install_path }}/addons'
```

### kubeone_apiserver_host

Domain or address of the Kubernetes API

#### Default value

```YAML
kubeone_apiserver_host:
```

### kubeone_apiserver_port

Port of the Kubernetes API

#### Default value

```YAML
kubeone_apiserver_port: 6443
```

### kubeone_apiserver_sans

Additional domains or addresses for the Kubernetes API

#### Default value

```YAML
kubeone_apiserver_sans: []
```

### kubeone_cloud_provider

Configuration for the cloud provider

#### Default value

```YAML
kubeone_cloud_provider: |
  none: {}
```

### kubeone_cluster_name

Name of the Kubernetes cluster

#### Default value

```YAML
kubeone_cluster_name:
```

### kubeone_cni_config

Configuration for the CNI provider

#### Default value

```YAML
kubeone_cni_config: |
  mtu: 1450
```

### kubeone_cni_provider

CNI provider to use

#### Default value

```YAML
kubeone_cni_provider: canal
```

### kubeone_config_content

Content of the cluster configuration

#### Default value

```YAML
kubeone_config_content: |
  apiVersion: kubeone.k8c.io/{{ kubeone_manifest_version }}
  kind: KubeOneCluster
  name: {{ kubeone_cluster_name }}

  versions:
    kubernetes: {{ kubeone_kubernetes_version }}

  apiEndpoint:
    host: {{ kubeone_apiserver_host }}
    port: {{ kubeone_apiserver_port }}
    alternativeNames: {{ kubeone_apiserver_sans | to_yaml }}

  machineController:
    deploy: {{ kubeone_machine_controller }}

  systemPackages:
    configureRepositories: {{ kubeone_configure_repositories }}

  clusterNetwork:
    podSubnet: {{ kubeone_pod_subnet }}
    serviceSubnet: {{ kubeone_service_subnet }}
    serviceDomainName: {{ kubeone_domain_name }}
    nodePortRange: {{ kubeone_node_ports }}
    cni:
      {{ kubeone_cni_provider }}:
        {{ kubeone_cni_config | from_yaml | to_nice_yaml(indent=2) | indent(width=6, first=False) | trim }}
  {% if kubeone_cloud_provider | default(False) %}

  cloudProvider:
    {{ kubeone_cloud_provider | from_yaml | to_nice_yaml(indent=2) | indent(width=2, first=False) | trim }}
  {% endif %}
  {% if kubeone_control_plane | default(False) %}

  controlPlane:
    hosts:
      {{ kubeone_control_plane | from_yaml | to_nice_yaml(indent=2) | indent(width=4, first=False) | trim }}
  {% endif %}
  {% if kubeone_static_workers | default(False) %}

  staticWorkers:
    hosts:
      {{ kubeone_static_workers | from_yaml | to_nice_yaml(indent=2) | indent(width=4, first=False) | trim }}
  {% endif %}
  {% if kubeone_dynamic_workers | default(False) %}

  dynamicWorkers:
    {{ kubeone_dynamic_workers | from_yaml | to_nice_yaml(indent=2) | indent(width=2, first=False) | trim }}
  {% endif %}

  features:
  {% if kubeone_openid_connect_enable | default(False) %}
    openidConnect:
      enable: {{ kubeone_openid_connect_enable }}
  {% if kubeone_openid_connect_config | default(False) %}
      config:
        {{ kubeone_openid_connect_config | from_yaml | to_nice_yaml(indent=2) | indent(width=6, first=False) | trim }}
  {% endif %}
  {% endif %}
  {% if kubeone_encryption_providers_enable | default(False) %}
    encryptionProviders:
      enable: {{ kubeone_encryption_providers_enable }}
  {% if kubeone_encryption_providers_config | default(False) %}
      customEncryptionConfiguration:
        {{ kubeone_encryption_providers_config | from_yaml | to_nice_yaml(indent=2) | indent(width=6, first=False) | trim }}
  {% endif %}
  {% endif %}
  {% if kubeone_pod_node_selector_enable | default(False) %}
    podNodeSelector:
      enable: {{ kubeone_pod_node_selector_enable }}
  {% if kubeone_pod_node_selector_config | default(False) %}
      config:
        {{ kubeone_pod_node_selector_config | from_yaml | to_nice_yaml(indent=2) | indent(width=6, first=False) | trim }}
  {% endif %}
  {% endif %}
  {% if kubeone_static_auditlog_enable | default(False) %}
    staticAuditLog:
      enable: {{ kubeone_static_auditlog_enable }}
  {% if kubeone_static_auditlog_config | default(False) %}
      config:
        {{ kubeone_static_auditlog_config | from_yaml | to_nice_yaml(indent=2) | indent(width=6, first=False) | trim }}
  {% endif %}
  {% endif %}
    dynamicAuditLog:
      enable: {{ kubeone_dynamic_auditlog_enable }}
    metricsServer:
      enable: {{ kubeone_metrics_server_enable }}

  addons:
    enable: {{ kubeone_addons_enable }}
    path: {{ kubeone_addons_path }}
  {% if kubeone_addons_general + kubeone_addons_extra | default(False) %}
    addons:
  {% for item in kubeone_addons_general + kubeone_addons_extra %}
      - name: {{ item.name }}
  {% if item.params | default(False) %}
        params:
          {{ item.params | to_nice_yaml(indent=2) | indent(width=8, first=False) }}
  {% endif %}
        delete: {{ item.delete | default(False) }}
  {% endfor %}
  {% endif %}
```

### kubeone_config_path

Path to cluster configuration

#### Default value

```YAML
kubeone_config_path: /etc/kubeone/cluster.yml
```

### kubeone_configure_repositories

Configure repositories for system packages

#### Default value

```YAML
kubeone_configure_repositories: true
```

### kubeone_control_plane

Host list for control plane

#### Default value

```YAML
kubeone_control_plane: []
```

#### Example usage

```YAML
kubeone_control_plane:
  - publicAddress: 192.168.1.10
    sshUsername: oper
    sshPrivateKeyFile: /path/to/private/key
  - publicAddress: 192.168.1.11
    sshUsername: oper
    sshPrivateKeyFile: /path/to/private/key
  - publicAddress: 192.168.1.12
    sshUsername: oper
    sshPrivateKeyFile: /path/to/private/key
```

### kubeone_domain_name

Cluster domain name

#### Default value

```YAML
kubeone_domain_name: cluster.local
```

### kubeone_dynamic_auditlog_enable

Enable dynamic auditlog feature

#### Default value

```YAML
kubeone_dynamic_auditlog_enable: false
```

### kubeone_dynamic_workers

Config list for dynamic workers

#### Default value

```YAML
kubeone_dynamic_workers: []
```

#### Example usage

```YAML
kubeone_dynamic_workers:
  - name: worker1
    replicas: 5
    providerSpec:
      ...
  - name: worker2
    replicas: 3
    providerSpec:
      ...
```

### kubeone_encryption_providers_config

Configuration for encrpytion providers

#### Default value

```YAML
kubeone_encryption_providers_config:
```

### kubeone_encryption_providers_enable

Enable encryption provider feature

#### Default value

```YAML
kubeone_encryption_providers_enable: true
```

### kubeone_environment_variables

Environment variables used by KubeOne

#### Default value

```YAML
kubeone_environment_variables:
```

### kubeone_force_apply

Force apply even if config has not changed

#### Default value

```YAML
kubeone_force_apply: false
```

### kubeone_force_install

Force install on next apply

#### Default value

```YAML
kubeone_force_install: false
```

### kubeone_force_upgrade

Force upgrade on next apply

#### Default value

```YAML
kubeone_force_upgrade: false
```

### kubeone_install_path

Installation path for the release

#### Default value

```YAML
kubeone_install_path: /usr/share/kubeone-{{ kubeone_release_version }}
```

### kubeone_kubernetes_version

Kubernetes version to install

#### Default value

```YAML
kubeone_kubernetes_version: 1.26.1
```

### kubeone_log_path

Path to logfile where apply output gets written to

#### Default value

```YAML
kubeone_log_path: /var/log/kubeone{{ '-' + kubeone_cluster_name if kubeone_cluster_name
  | default(False) else '' }}.log
```

### kubeone_machine_controller

Install the machine controller

#### Default value

```YAML
kubeone_machine_controller: true
```

### kubeone_manifest_version

Manifest version for the KubeOne configuration

#### Default value

```YAML
kubeone_manifest_version: v1beta2
```

### kubeone_metrics_server_enable

Enable metrics server feature

#### Default value

```YAML
kubeone_metrics_server_enable: true
```

### kubeone_node_ports

Node port range

#### Default value

```YAML
kubeone_node_ports: 30000-32767
```

### kubeone_openid_connect_config

Configuration for OpenID Connect

#### Default value

```YAML
kubeone_openid_connect_config:
```

### kubeone_openid_connect_enable

Enable OpenID Connect feature

#### Default value

```YAML
kubeone_openid_connect_enable: false
```

### kubeone_pod_node_selector_config

Configuration for pod node selector

#### Default value

```YAML
kubeone_pod_node_selector_config:
```

### kubeone_pod_node_selector_enable

Enable pod node selector feature

#### Default value

```YAML
kubeone_pod_node_selector_enable: false
```

### kubeone_pod_subnet

Pod subnet within Kubernetes

#### Default value

```YAML
kubeone_pod_subnet: 10.244.0.0/16
```

### kubeone_release_download

URL to download the KubeOne release from

#### Default value

```YAML
kubeone_release_download: https://github.com/kubermatic/kubeone/releases/download/v{{
  kubeone_release_version }}/kubeone_{{ kubeone_release_version }}_linux_amd64.zip
```

### kubeone_release_version

Version of KubeOne to download and use

#### Default value

```YAML
kubeone_release_version: 1.5.6
```

### kubeone_rotate_encryption_key

Rotate encryption keys on next apply

#### Default value

```YAML
kubeone_rotate_encryption_key: false
```

### kubeone_service_subnet

Service subnet within Kubernetes

#### Default value

```YAML
kubeone_service_subnet: 10.96.0.0/12
```

### kubeone_static_auditlog_config

Configuration for static auditlog

#### Default value

```YAML
kubeone_static_auditlog_config:
```

### kubeone_static_auditlog_enable

Enable static auditlog feature

#### Default value

```YAML
kubeone_static_auditlog_enable: false
```

### kubeone_static_workers

Host list for static workers

#### Default value

```YAML
kubeone_static_workers: []
```

#### Example usage

```YAML
kubeone_static_workers:
  - publicAddress: 192.168.1.10
    sshUsername: oper
    sshPrivateKeyFile: /path/to/private/key
  - publicAddress: 192.168.1.11
    sshUsername: oper
    sshPrivateKeyFile: /path/to/private/key
  - publicAddress: 192.168.1.12
    sshUsername: oper
    sshPrivateKeyFile: /path/to/private/key
```

### kubeone_upgrade_machine_deployments

Upgrade machine deployments on next apply

#### Default value

```YAML
kubeone_upgrade_machine_deployments: true
```

## Discovered Tags

**_kubeone_**

**_skip_ansible_later_**


## Dependencies

- None

## License

Apache-2.0

## Author

[Thomas Boerger](https://github.com/tboerger)
