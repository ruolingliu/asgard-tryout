# Syncer

`asgard-ai.com/v1alpha1`, kind `Syncer`, plural `syncers`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.bot` | object | - |  |  |  |
| `spec.bot.botProviderName` | string | **required** |  |  |  |
| `spec.bot.messageFilter` | object | - |  |  |  |
| `spec.bot.messageFilter.includeBot` | boolean | **required** |  |  |  |
| `spec.bot.messageFilter.includeUser` | boolean | **required** |  |  |  |
| `spec.bot.messageFilter.minLength` | integer | **required** |  | format `int32` |  |
| `spec.database` | object | - |  |  |  |
| `spec.database.batchSize` | integer | **required** |  | format `int32` |  |
| `spec.database.columns` | array | **required** |  |  |  |
| `spec.database.columns[].isIdentifier` | boolean | - |  |  |  |
| `spec.database.columns[].isMaxValueColumn` | boolean | - |  |  |  |
| `spec.database.columns[].name` | string | **required** |  | matches `^[a-zA-Z_][a-zA-Z0-9_]*$` |  |
| `spec.database.dataConnectorName` | string | **required** |  |  |  |
| `spec.database.query` | string | **required** |  |  |  |
| `spec.destinationMemberKey` | string | - |  | **deprecated** | Deprecated: use destinationPath instead. Kept only so pre-rename Syncer objects stay readable during the transition; new objects should set destinationPath. |
| `spec.destinationPath` | string | - |  |  | Relative path within the SourceSet volume that this Syncer writes into. There is no root inside the volume, so the path must not start with '/'. For every class but static-content it denotes a directory and must end with '/'; for static-content it is the one file the Syncer writes and must not. Whether it may end with '/' depends on syncerClass, which a rule on this field cannot see, so that check sits on the spec. Each syncerClass validates the expected shape at runtime. |
| `spec.dropbox` | object | - |  |  |  |
| `spec.dropbox.folderPath` | string | **required** |  |  |  |
| `spec.dropbox.oAuthCredentialName` | string | **required** |  |  |  |
| `spec.dropbox.recursive` | boolean | - |  |  |  |
| `spec.ftp` | object | - |  |  |  |
| `spec.ftp.host` | string | **required** |  |  |  |
| `spec.ftp.noCheckCertificate` | boolean | - |  |  | Do not verify the TLS certificate of the server. |
| `spec.ftp.password` | object | **required** |  |  |  |
| `spec.ftp.password.value` | string | - |  |  |  |
| `spec.ftp.password.valueFrom` | object | - |  |  |  |
| `spec.ftp.password.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.ftp.password.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.ftp.password.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.ftp.password.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.ftp.password.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.ftp.password.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.ftp.password.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.ftp.password.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.ftp.port` | integer | - |  | format `int32` |  |
| `spec.ftp.recursive` | boolean | - |  |  |  |
| `spec.ftp.remotePath` | string | **required** |  |  |  |
| `spec.ftp.useExplicitTls` | boolean | - |  |  | Use explicit FTPS (FTP over TLS). Client upgrades plain connection to encrypted. |
| `spec.ftp.useTls` | boolean | - |  |  | Use implicit FTPS (FTP over TLS). Default port becomes 990. |
| `spec.ftp.username` | object | **required** |  |  |  |
| `spec.ftp.username.value` | string | - |  |  |  |
| `spec.ftp.username.valueFrom` | object | - |  |  |  |
| `spec.ftp.username.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.ftp.username.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.ftp.username.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.ftp.username.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.ftp.username.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.ftp.username.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.ftp.username.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.ftp.username.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.git` | object | - |  |  |  |
| `spec.git.auth` | object | - |  |  | Optional authentication for private repositories. Currently only http type is supported. |
| `spec.git.auth.password` | object | **required** |  |  |  |
| `spec.git.auth.password.value` | string | - |  |  |  |
| `spec.git.auth.password.valueFrom` | object | - |  |  |  |
| `spec.git.auth.password.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.git.auth.password.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.git.auth.password.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.git.auth.password.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.git.auth.password.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.git.auth.password.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.git.auth.password.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.git.auth.password.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.git.auth.type` | string | **required** |  | one of `http`, `ssh` |  |
| `spec.git.auth.username` | object | - |  |  |  |
| `spec.git.auth.username.value` | string | - |  |  |  |
| `spec.git.auth.username.valueFrom` | object | - |  |  |  |
| `spec.git.auth.username.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.git.auth.username.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.git.auth.username.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.git.auth.username.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.git.auth.username.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.git.auth.username.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.git.auth.username.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.git.auth.username.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.git.includePaths` | array | - |  |  | IncludePaths narrows the checkout to these folders of the repository. Absent or empty syncs the whole repository, exactly as before. The point is a large repository of which only a few folders matter: only those folders are downloaded, written to the volume, and kept in the checkout's .git. Each entry is one folder, relative to the repository root and written like a Syncer's destinationPath — "docs/": no leading '/', a trailing '/', no '.' or '..' segment. It includes everything beneath it. - LITERAL folder names, never globs: "*" matches only a folder named "*". - Several entries are a union; one beneath another is redundant, not an error. - Folders keep their place in the repository layout: "docs/" lands at <destinationPath>docs/, not at <destinationPath>. - Git's cone mode also brings the files sitting directly in the repository root, and directly in every parent folder of an entry: "a/b/" brings a/'s own files too, but not a/c/. - Every entry must be a folder at the synced revision. If one is missing, or is a file, the run fails and the destination is left untouched. - Editable at any time; the next run converges in place. Widening downloads only the added folders, narrowing removes the dropped ones and frees their space, and clearing the list turns it back into a full checkout — none of it re-clones the repository. - The bandwidth saving needs a git server with partial clone support (GitHub, GitLab, Gitea/Forgejo, ...). Against one without it the sync still works and the destination still holds only these folders; git just downloads more. The '.' / '..' rule checks whole segments, unlike destinationPath's substring check, so a folder legitimately named "Acme Inc." stays expressible. |
| `spec.git.repoUrl` | string | **required** |  |  |  |
| `spec.git.revision` | string | **required** |  |  |  |
| `spec.googleDrive` | object | - |  |  |  |
| `spec.googleDrive.folderId` | string | **required** |  |  |  |
| `spec.googleDrive.oAuthCredentialName` | string | **required** |  |  |  |
| `spec.googleDrive.recursive` | boolean | - |  |  |  |
| `spec.oneDrive` | object | - |  |  |  |
| `spec.oneDrive.folderId` | string | - |  |  |  |
| `spec.oneDrive.folderPath` | string | - |  |  |  |
| `spec.oneDrive.oAuthCredentialName` | string | **required** |  |  |  |
| `spec.oneDrive.recursive` | boolean | - |  |  |  |
| `spec.schedule` | string | **required** |  |  |  |
| `spec.sftp` | object | - |  |  |  |
| `spec.sftp.checkers` | integer | - |  | format `int32` | Checkers is how many files the sync compares in parallel when deciding what changed. Unlike transfers, raising this past the remote's comfort point makes the scan slower rather than faster, so measure before changing it. Leave unset to take the platform default. |
| `spec.sftp.host` | string | **required** |  |  |  |
| `spec.sftp.password` | object | - |  |  |  |
| `spec.sftp.password.value` | string | - |  |  |  |
| `spec.sftp.password.valueFrom` | object | - |  |  |  |
| `spec.sftp.password.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.sftp.password.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.sftp.password.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.sftp.password.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.sftp.password.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.sftp.password.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.sftp.password.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.sftp.password.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.sftp.port` | integer | - |  | format `int32` |  |
| `spec.sftp.privateKey` | object | - |  |  |  |
| `spec.sftp.privateKey.value` | string | - |  |  |  |
| `spec.sftp.privateKey.valueFrom` | object | - |  |  |  |
| `spec.sftp.privateKey.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.sftp.privateKey.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.sftp.privateKey.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.sftp.privateKey.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.sftp.privateKey.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.sftp.privateKey.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.sftp.privateKey.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.sftp.privateKey.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.sftp.recursive` | boolean | - |  |  |  |
| `spec.sftp.remotePath` | string | **required** |  |  |  |
| `spec.sftp.transfers` | integer | - |  | format `int32` | Transfers is how many files the sync moves in parallel. Leave unset to take the platform default; set it when this particular SFTP server cannot take that much concurrency — a small NAS, a rate-limited managed SFTP endpoint, or anything fronted by fail2ban — or when it can take more. The right value is a property of the remote, not of the platform, which is why it lives here. |
| `spec.sftp.username` | object | **required** |  |  |  |
| `spec.sftp.username.value` | string | - |  |  |  |
| `spec.sftp.username.valueFrom` | object | - |  |  |  |
| `spec.sftp.username.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.sftp.username.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.sftp.username.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.sftp.username.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.sftp.username.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.sftp.username.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.sftp.username.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.sftp.username.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.smb` | object | - |  |  |  |
| `spec.smb.domain` | object | - |  |  |  |
| `spec.smb.domain.value` | string | - |  |  |  |
| `spec.smb.domain.valueFrom` | object | - |  |  |  |
| `spec.smb.domain.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.smb.domain.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.smb.domain.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.smb.domain.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.smb.domain.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.smb.domain.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.smb.domain.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.smb.domain.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.smb.host` | string | **required** |  |  |  |
| `spec.smb.password` | object | **required** |  |  |  |
| `spec.smb.password.value` | string | - |  |  |  |
| `spec.smb.password.valueFrom` | object | - |  |  |  |
| `spec.smb.password.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.smb.password.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.smb.password.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.smb.password.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.smb.password.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.smb.password.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.smb.password.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.smb.password.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.smb.port` | integer | - |  | format `int32` |  |
| `spec.smb.recursive` | boolean | - |  |  |  |
| `spec.smb.remotePath` | string | **required** |  |  |  |
| `spec.smb.username` | object | **required** |  |  |  |
| `spec.smb.username.value` | string | - |  |  |  |
| `spec.smb.username.valueFrom` | object | - |  |  |  |
| `spec.smb.username.valueFrom.configMapKeyRef` | object | - |  |  | Selects a key from a ConfigMap. |
| `spec.smb.username.valueFrom.configMapKeyRef.key` | string | **required** |  |  | The key to select. |
| `spec.smb.username.valueFrom.configMapKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.smb.username.valueFrom.configMapKeyRef.optional` | boolean | - |  |  | Specify whether the ConfigMap or its key must be defined |
| `spec.smb.username.valueFrom.secretKeyRef` | object | - |  |  | SecretKeySelector selects a key of a Secret. |
| `spec.smb.username.valueFrom.secretKeyRef.key` | string | **required** |  |  | The key of the secret to select from. Must be a valid secret key. |
| `spec.smb.username.valueFrom.secretKeyRef.name` | string | - | `""` |  | Name of the referent. This field is effectively required, but due to backwards compatibility is allowed to be empty. Instances of this type with an empty value here are almost certainly wrong. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names |
| `spec.smb.username.valueFrom.secretKeyRef.optional` | boolean | - |  |  | Specify whether the Secret or its key must be defined |
| `spec.sourceSetName` | string | **required** |  | matches `^[a-z0-9][a-z0-9\-]*$` | Name of the SourceSet to sync into. Must already exist. |
| `spec.stateMemberKey` | string | - |  | **deprecated** | Deprecated: use statePath instead. Kept only so pre-rename Syncer objects stay readable during the transition; new objects should set statePath. |
| `spec.statePath` | string | - |  |  | Optional relative file path within the SourceSet volume where the Syncer runtime writes its sync-state file after each sync. |
| `spec.staticContent` | object | - |  |  | StaticContentSyncerSpec makes the Syncer keep exactly one file in the SourceSet volume: the file at destinationPath, which for this class names a file and does not end with '/', holds Text byte for byte. Each run compares the file on the volume with Text and leaves it alone when they match, so an unchanged file keeps its size and modification time. A file that differs is replaced as a whole, including one someone edited by hand: the Syncer wins on its next run. Missing parent directories are created. The run fails and writes nothing when the path cannot hold the file: a parent that has to be a directory is a file, the file itself is a directory, or any part of the path is a symlink. Deleting the Syncer leaves the file where it is. One Syncer writes one file, on purpose. Several files, or anything with structure, belong in a git repository synced by a git Syncer. Text has no length limit of its own; the whole Syncer object is bounded by the Kubernetes object size limit. |
| `spec.staticContent.text` | string | **required** |  |  | Text is the file's entire content, written as is: no trailing newline is added or removed. Empty is allowed and yields an empty file. |
| `spec.syncerClass` | string | **required** |  | one of `web`, `database`, `bot`, `google-drive`, `onedrive`, `git`, `dropbox`, `ftp`, `sftp`, `smb`, `static-content` |  |
| `spec.timeZone` | string | **required** |  |  |  |
| `spec.web` | object | - |  |  |  |
| `spec.web.delayMs` | integer | - |  | format `int64` |  |
| `spec.web.limitPerUrl` | integer | - |  | format `int64` |  |
| `spec.web.maxDepth` | integer | - |  | format `int64` |  |
| `spec.web.siteMapUrl` | string | - |  |  | Sitemap URL to crawl for web sync (use this instead of urls) |
| `spec.web.timeoutMs` | integer | **required** |  | format `int64` |  |
| `spec.web.urls` | array | - |  |  |  |
| `spec.web.waitForMs` | integer | **required** |  | format `int64` |  |
