# amq-broker-config

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 7.13.3](https://img.shields.io/badge/AppVersion-7.13.3-informational?style=flat-square)

Helm chart to deploy an ArtemisMQ instance using Red Hat AMQ Broker Operator

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Sarafou Balde | <sbalde@redhat.com> | <https://www.redhat.com> |
| Fraser Walker | <fwalker@redhat.com> | <https://www.redhat.com> |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| authentication | object | See child keys | Control authentication configurations for Red Hat AMQ Broker |
| authentication.clientCertificateAuthentication.clientCertSecretName | string | `nil` | Name of the secret that stores a trust bundle of client  certificates and the CA certificate to trust. |
| authentication.clientCertificateAuthentication.enabled | bool | `false` | Enable Client Certificate Authentication |
| authentication.disable | bool | `false` | Disable authentication. Not recommended for production. |
| authentication.ldapRealm | object | See child keys | Control LDAP Security Realm Configuration. This will result in a custom configuration being created as a `ConfigMap` |
| authentication.ldapRealm.connectionTimeout | int | `5000` | Sets the timeout, in milliseconds, for LDAP server connections. |
| authentication.ldapRealm.credentialAlias | string | `nil` | Name of the key from the `secret` that contains the password used to connect to the LDAP server |
| authentication.ldapRealm.credentialSecret | string | `nil` | Name of the `secret` that contains the password used to connect to the LDAP server |
| authentication.ldapRealm.enabled | bool | `false` | Enable LDAP security realm |
| authentication.ldapRealm.principal | string | `nil` | Specifies the user principal for LDAP server connections |
| authentication.ldapRealm.readTimeout | int | `5000` | Sets the read timeout, in milliseconds, for LDAP server operations. |
| authentication.ldapRealm.url | string | `nil` | Specifies the URL for LDAP server connections in the format ldap[s]://{hostname}:{port} |
| authentication.ldapRealm.userBase | string | `nil` | Sets the Base DN for Users |
| authentication.propertiesRealm | object | See child keys | Control Properties Security Realm Configuration when using multiple security realms |
| authentication.propertiesRealm.credentialsSecretName | string | `nil` | Name of the `Secret` containing an users and roles declaration used to configure a properties realm. There must be an entry with key `custom-users.properties` and contents in the format of 'username = password' and an entry with key `custom-roles.properties` in the format of 'role = user1,user2...' |
| authentication.propertiesRealm.enabled | bool | `true` | Enable properties security realm |
| authorization | object | See child keys | Control authorization for Red Hat AMQ Broker. |
| authorization.customRoles | object | See child keys | Custom RBAC roles permission configuration. |
| authorization.customRoles.enabled | bool | `false` | Enable custom role configuration. |
| authorization.customRoles.roles | object | See example role entry. Will emit entries in the format | List of custom role configurations. of <address>.<resource name>.<operation> |
| authorization.customRoles.roles.admin | list | `[{"address":"#","browse":true,"consume":true,"createAddress":true,"createDurableQueue":true,"createNonDurableQueue":true,"deleteAddress":true,"deleteDurableQueue":true,"deleteNonDurableQueue":true,"manage":true,"send":true,"view":true}]` | Name of the custom role |
| authorization.customRoles.roles.admin[0] | object | `{"address":"#","browse":true,"consume":true,"createAddress":true,"createDurableQueue":true,"createNonDurableQueue":true,"deleteAddress":true,"deleteDurableQueue":true,"deleteNonDurableQueue":true,"manage":true,"send":true,"view":true}` | A list of permissions for a role. Address field must exist. |
| authorization.customRoles.roles.admin[0].createNonDurableQueue | bool | `true` | Resource Name as key and Operation as value |
| authorization.enabled | bool | `false` | Enable authorization to provide more granular security control over the Red Hat AMQ Broker. |
| availability | object | See child keys | Control high availability for Red Hat AMQ Broker |
| availability.antiAffinitityType | string | `"required"` | One of `preferred`, for `preferredDuringSchedulingIgnoredDuringExecution`, or `required`, for `requiredDuringSchedulingIgnoredDuringExecution`, modes. |
| availability.enabled | bool | `false` | Enable high availability using anti-affinity. |
| availability.hostname | bool | `true` | Use `kubernetes.io/hostname` `topologyKey` |
| availability.zone | bool | `false` | Use `topology.kubernetes.io/zone` `topologyKey` |
| broker | object | See child keys | Settings related to the Red Hat AMQ Broker |
| broker.console | object | See child keys | Control console configurations for Red Hat AMQ Broker |
| broker.console.customDomain | string | `nil` | Custom domain for the console. Refer to https://docs.redhat.com/en/documentation/red_hat_amq_broker/7.13/html-single/deploying_amq_broker_on_openshift/index#proc-br-enabling-console-access_broker-ocp for configuration details |
| broker.console.customHost | string | `nil` | Custom host name for the console. Refer to https://docs.redhat.com/en/documentation/red_hat_amq_broker/7.13/html-single/deploying_amq_broker_on_openshift/index#proc-br-enabling-console-access_broker-ocp for configuration details |
| broker.console.expose | bool | `true` | create a route or ingress to expose the console |
| broker.console.tls | object | See child keys | TLS/SSL settings for the console ingress |
| broker.console.tls.sslEnabled | bool | `true` | Enable TLS/SSL for the console ingress |
| broker.console.tls.sslSecret | string | `"default-ssl"` | The name of the TLS secret for the console. |
| broker.deploymentPlan | object | See child keys | Settings related to the Deployment Plan for the Broker |
| broker.deploymentPlan.replicas | int | `1` | The number of broker pods to deploy. |
| broker.enabled | boolean | `true` | Create an `ActiveMQArtemis` resource for the Red Hat AMQ Broker Operator |
| broker.labels | object | `{"app":"amq-broker"}` | Labels to apply to the broker resources. |
| broker.name | string | `"amq"` | The name of the ActiveMQArtemis custom resource. |
| encryption | object | See child keys | Control encryption configurations for Red Hat AMQ Broker |
| encryption.certSecretName | string | `nil` | Name of the secret containing the custom TLS/SSL certificate and key |
| encryption.disable | bool | `false` | Disable encryption. Not recommended for production. |
| logging | object | See child keys | Control log level for categories for Red Hat AMQ Broker |
| monitoring | object | See child keys | Control monitoring configurations for Red Hat AMQ Broker |
| monitoring.enablePrometheus | bool | `true` | Disable the default prometheus service monitor |
| monitoring.enableServiceMonitor | bool | `false` | Create a `ServiceMonitor` to collect metrics. |
| operator | object | See child keys | Settings related to the Red Hat AMQ Broker Operator `Subscription` |
| operator.channel | string | `"7.13.x"` | The `channel` of the Operator |
| operator.enabled | boolean | `false` | Create a `Subscription` for the Red Hat AMQ Broker Operator |
| operator.installNamespace | string | `"openshift-operators"` | The `Namespace` the Operator will be deployed in |
| operator.managedNamespaces | list | `[]` | When `operator.singleInstance` is marked as false, this instance of the  Operator will manage these namespaces |
| operator.singleInstance | boolean | `true` | Use a single operator instance to manage all Red Hat AMQ Broker  instances |
| operator.startingCSV | string | `nil` | The minimum `ClusterServiceVersion` for the operator |
| operator.updateApproval | string | `"Manual"` | Set the `Subscription` update approval mode. `Manual` will require install plans to be approved before upgrades will take place (recommended  for Production installations) while `Automatic` will be applied as and when they become available |
| resources | object | See child keys | Control resource configurations for Red Hat AMQ Broker |
| resources.limits | object | See child keys | A limit sets the maximum amount of a resource (CPU or memory) that a container is allowed to consume. |
| resources.limits.cpu | string | `"1000m"` | The maximum amount of CPU the application is allowed to use. |
| resources.limits.memory | string | `"1Gi"` | The maximum amount of memory the application is allowed to use. |
| resources.requests | object | See child keys | A request specifies the minimum amount of a resource (CPU or memory) that Kubernetes guarantees for a container. |
| resources.requests.cpu | string | `"250m"` | The amount of CPU guaranteed for the application to use. |
| resources.requests.memory | string | `"1Gi"` | The amount of memory guaranteed for the application to use. |

