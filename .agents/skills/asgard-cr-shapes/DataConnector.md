# DataConnector

`asgard-ai.com/v1alpha1`, kind `DataConnector`, plural `dataconnectors`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.athena` | object | - |  |  |  |
| `spec.athena.accessKeyId` | object | **required** |  |  |  |
| `spec.athena.accessKeyId.value` | string | - |  |  |  |
| `spec.athena.accessKeyId.valueFrom` | object | - |  |  |  |
| `spec.athena.accessKeyId.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.athena.accessKeyId.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.athena.accessKeyId.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.athena.accessKeyId.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.athena.accessKeyId.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.athena.accessKeyId.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.athena.accessKeyId.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.athena.accessKeyId.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.athena.outputLocation` | string | **required** |  |  |  |
| `spec.athena.region` | string | **required** |  |  |  |
| `spec.athena.secretAccessKey` | object | **required** |  |  |  |
| `spec.athena.secretAccessKey.value` | string | - |  |  |  |
| `spec.athena.secretAccessKey.valueFrom` | object | - |  |  |  |
| `spec.athena.secretAccessKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.athena.secretAccessKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.athena.secretAccessKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.athena.secretAccessKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.athena.secretAccessKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.athena.secretAccessKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.athena.secretAccessKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.athena.secretAccessKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.athena.workGroup` | string | - |  |  |  |
| `spec.dataConnectorClass` | string | **required** |  | one of `postgres`, `mysql`, `mssql`, `oracle`, `salesforce`, `hana`, `netsuite`, `trino`, `athena` |  |
| `spec.hana` | object | - |  |  |  |
| `spec.hana.host` | string | **required** |  |  |  |
| `spec.hana.password` | object | **required** |  |  |  |
| `spec.hana.password.value` | string | - |  |  |  |
| `spec.hana.password.valueFrom` | object | - |  |  |  |
| `spec.hana.password.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.hana.password.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.hana.password.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.hana.password.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.hana.password.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.hana.password.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.hana.password.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.hana.password.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.hana.port` | integer | **required** |  | format `int32` |  |
| `spec.hana.user` | string | **required** |  |  |  |
| `spec.mssql` | object | - |  |  |  |
| `spec.mssql.database` | string | **required** |  |  |  |
| `spec.mssql.host` | string | **required** |  |  |  |
| `spec.mssql.instance` | string | - |  |  |  |
| `spec.mssql.password` | object | **required** |  |  |  |
| `spec.mssql.password.value` | string | - |  |  |  |
| `spec.mssql.password.valueFrom` | object | - |  |  |  |
| `spec.mssql.password.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.mssql.password.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.mssql.password.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.mssql.password.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.mssql.password.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.mssql.password.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.mssql.password.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.mssql.password.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.mssql.port` | integer | **required** |  | format `int32` |  |
| `spec.mssql.tlsMaxVersion` | string | - |  | one of `1.0`, `1.1` | TlsMaxVersion caps the TLS version for a legacy SQL Server. LEAVE UNSET unless tlsMinVersion's description matches your situation exactly; it is only meaningful together with tlsMinVersion. A cap on a current server that only accepts TLS 1.2 or newer makes the connection fail outright, and a cap left in place after the server is upgraded keeps the connection on TLS 1.1 or 1.0 until someone removes it. |
| `spec.mssql.tlsMinVersion` | string | - |  | one of `1.0`, `1.1` | TlsMinVersion lowers the TLS floor for a legacy SQL Server. LEAVE UNSET unless you have the exact problem below; almost no DataConnector needs it. Unset means the driver default (TLS 1.2 or newer), which is correct for every reasonably current server. The one case it exists for: an old SQL Server whose TLS stack cannot complete a TLS 1.2 handshake without SHA-1 signatures (e.g. SQL Server 2012 on an old Windows Schannel). Connection tests then fail with TLS Handshake failed: cannot read handshake packet: EOF even though host, port and credentials are known to be correct. For that case set tlsMinVersion "1.0" and tlsMaxVersion "1.1". It does NOT fix wrong credentials (SQL Server error 18456 "Login failed"), timeouts, firewall or DNS problems; setting it for those only weakens the connection. It affects this DataConnector only, and the connection will negotiate TLS 1.1 or 1.0. Remove it once the server is upgraded. It relies on the client still supporting TLS 1.0/1.1, which FIPS mode does not. |
| `spec.mssql.user` | string | **required** |  |  |  |
| `spec.mysql` | object | - |  |  |  |
| `spec.mysql.database` | string | **required** |  |  |  |
| `spec.mysql.host` | string | **required** |  |  |  |
| `spec.mysql.password` | object | **required** |  |  |  |
| `spec.mysql.password.value` | string | - |  |  |  |
| `spec.mysql.password.valueFrom` | object | - |  |  |  |
| `spec.mysql.password.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.mysql.password.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.mysql.password.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.mysql.password.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.mysql.password.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.mysql.password.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.mysql.password.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.mysql.password.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.mysql.port` | integer | **required** |  | format `int32` |  |
| `spec.mysql.user` | string | **required** |  |  |  |
| `spec.netsuite` | object | - |  |  |  |
| `spec.netsuite.certificateId` | string | **required** |  |  |  |
| `spec.netsuite.consumerKey` | object | **required** |  |  |  |
| `spec.netsuite.consumerKey.value` | string | - |  |  |  |
| `spec.netsuite.consumerKey.valueFrom` | object | - |  |  |  |
| `spec.netsuite.consumerKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.netsuite.consumerKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.netsuite.consumerKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.netsuite.consumerKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.netsuite.consumerKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.netsuite.consumerKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.netsuite.consumerKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.netsuite.consumerKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.netsuite.host` | string | **required** |  |  |  |
| `spec.netsuite.privateKeyPem` | object | **required** |  |  |  |
| `spec.netsuite.privateKeyPem.value` | string | - |  |  |  |
| `spec.netsuite.privateKeyPem.valueFrom` | object | - |  |  |  |
| `spec.netsuite.privateKeyPem.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.netsuite.privateKeyPem.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.netsuite.privateKeyPem.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.netsuite.privateKeyPem.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.netsuite.privateKeyPem.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.netsuite.privateKeyPem.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.netsuite.privateKeyPem.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.netsuite.privateKeyPem.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.netsuite.signatureAlgorithm` | string | **required** |  | one of `ES256`, `ES512`, `PS256` |  |
| `spec.oracle` | object | - |  |  |  |
| `spec.oracle.host` | string | **required** |  |  |  |
| `spec.oracle.password` | object | **required** |  |  |  |
| `spec.oracle.password.value` | string | - |  |  |  |
| `spec.oracle.password.valueFrom` | object | - |  |  |  |
| `spec.oracle.password.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.oracle.password.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.oracle.password.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.oracle.password.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.oracle.password.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.oracle.password.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.oracle.password.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.oracle.password.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.oracle.port` | integer | **required** |  | format `int32` |  |
| `spec.oracle.serviceName` | string | - |  |  |  |
| `spec.oracle.sid` | string | - |  |  |  |
| `spec.oracle.user` | string | **required** |  |  |  |
| `spec.postgres` | object | - |  |  |  |
| `spec.postgres.database` | string | **required** |  |  |  |
| `spec.postgres.host` | string | **required** |  |  |  |
| `spec.postgres.password` | object | **required** |  |  |  |
| `spec.postgres.password.value` | string | - |  |  |  |
| `spec.postgres.password.valueFrom` | object | - |  |  |  |
| `spec.postgres.password.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.postgres.password.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.postgres.password.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.postgres.password.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.postgres.password.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.postgres.password.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.postgres.password.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.postgres.password.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.postgres.port` | integer | **required** |  | format `int32` |  |
| `spec.postgres.sslMode` | string | - |  | one of `disable`, `require`, `verify-ca`, `verify-full` |  |
| `spec.postgres.user` | string | **required** |  |  |  |
| `spec.salesforce` | object | - |  |  |  |
| `spec.salesforce.consumerKey` | object | **required** |  |  |  |
| `spec.salesforce.consumerKey.value` | string | - |  |  |  |
| `spec.salesforce.consumerKey.valueFrom` | object | - |  |  |  |
| `spec.salesforce.consumerKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.salesforce.consumerKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.salesforce.consumerKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.salesforce.consumerKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.salesforce.consumerKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.salesforce.consumerKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.salesforce.consumerKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.salesforce.consumerKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.salesforce.consumerSecret` | object | **required** |  |  |  |
| `spec.salesforce.consumerSecret.value` | string | - |  |  |  |
| `spec.salesforce.consumerSecret.valueFrom` | object | - |  |  |  |
| `spec.salesforce.consumerSecret.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.salesforce.consumerSecret.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.salesforce.consumerSecret.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.salesforce.consumerSecret.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.salesforce.consumerSecret.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.salesforce.consumerSecret.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.salesforce.consumerSecret.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.salesforce.consumerSecret.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.salesforce.host` | string | **required** |  |  |  |
| `spec.sshTunnel` | object | - |  |  | SshTunnel, when set, routes every connection to the class-specific host:port through an SSH bastion (the equivalent of `ssh -L`): the bastion opens the TCP connection, so the database host is resolved and reached from the bastion's network. Only applies to classes that connect to a self-hosted endpoint. |
| `spec.sshTunnel.host` | string | **required** |  |  |  |
| `spec.sshTunnel.hostKey` | string | - |  |  | HostKey pins the bastion's public host key, one key per line, in authorized_keys (`ssh-ed25519 AAAA...`) or known_hosts / `ssh-keyscan` (`host ssh-ed25519 AAAA...`) format. When omitted the host key is not verified. |
| `spec.sshTunnel.password` | object | - |  |  |  |
| `spec.sshTunnel.password.value` | string | - |  |  |  |
| `spec.sshTunnel.password.valueFrom` | object | - |  |  |  |
| `spec.sshTunnel.password.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.sshTunnel.password.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.sshTunnel.password.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.sshTunnel.password.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.sshTunnel.password.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.sshTunnel.password.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.sshTunnel.password.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.sshTunnel.password.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.sshTunnel.port` | integer | - | `22` | format `int32` |  |
| `spec.sshTunnel.privateKey` | object | - |  |  | PrivateKey is a PEM-encoded private key (OpenSSH, PKCS#1, PKCS#8 or EC). |
| `spec.sshTunnel.privateKey.value` | string | - |  |  |  |
| `spec.sshTunnel.privateKey.valueFrom` | object | - |  |  |  |
| `spec.sshTunnel.privateKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.sshTunnel.privateKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.sshTunnel.privateKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.sshTunnel.privateKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.sshTunnel.privateKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.sshTunnel.privateKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.sshTunnel.privateKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.sshTunnel.privateKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.sshTunnel.privateKeyPassphrase` | object | - |  |  | PrivateKeyPassphrase decrypts PrivateKey when it is encrypted. |
| `spec.sshTunnel.privateKeyPassphrase.value` | string | - |  |  |  |
| `spec.sshTunnel.privateKeyPassphrase.valueFrom` | object | - |  |  |  |
| `spec.sshTunnel.privateKeyPassphrase.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.sshTunnel.privateKeyPassphrase.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.sshTunnel.privateKeyPassphrase.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.sshTunnel.privateKeyPassphrase.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.sshTunnel.privateKeyPassphrase.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.sshTunnel.privateKeyPassphrase.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.sshTunnel.privateKeyPassphrase.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.sshTunnel.privateKeyPassphrase.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.sshTunnel.user` | string | **required** |  |  |  |
| `spec.trino` | object | - |  |  |  |
| `spec.trino.host` | string | **required** |  |  |  |
| `spec.trino.jwtAccessToken` | object | - |  |  |  |
| `spec.trino.jwtAccessToken.value` | string | - |  |  |  |
| `spec.trino.jwtAccessToken.valueFrom` | object | - |  |  |  |
| `spec.trino.jwtAccessToken.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.trino.jwtAccessToken.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.trino.jwtAccessToken.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.trino.jwtAccessToken.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.trino.jwtAccessToken.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.trino.jwtAccessToken.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.trino.jwtAccessToken.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.trino.jwtAccessToken.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.trino.password` | object | - |  |  |  |
| `spec.trino.password.value` | string | - |  |  |  |
| `spec.trino.password.valueFrom` | object | - |  |  |  |
| `spec.trino.password.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.trino.password.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.trino.password.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.trino.password.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.trino.password.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.trino.password.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.trino.password.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.trino.password.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.trino.port` | integer | **required** |  | format `int32` |  |
| `spec.trino.scheme` | string | **required** |  | one of `http`, `https` |  |
| `spec.trino.sslCertificatePem` | object | - |  |  |  |
| `spec.trino.sslCertificatePem.value` | string | - |  |  |  |
| `spec.trino.sslCertificatePem.valueFrom` | object | - |  |  |  |
| `spec.trino.sslCertificatePem.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.trino.sslCertificatePem.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.trino.sslCertificatePem.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.trino.sslCertificatePem.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.trino.sslCertificatePem.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.trino.sslCertificatePem.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.trino.sslCertificatePem.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.trino.sslCertificatePem.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.trino.user` | string | **required** |  |  |  |
