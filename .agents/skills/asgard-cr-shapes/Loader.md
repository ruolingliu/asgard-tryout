# Loader

`asgard-ai.com/v1alpha1`, kind `Loader`, plural `loaders`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.bot` | object | - |  |  |  |
| `spec.bot.botProviderName` | string | **required** |  |  |  |
| `spec.bot.indexDocument` | object | - |  |  |  |
| `spec.bot.indexDocument.audio` | object | - |  |  |  |
| `spec.bot.indexDocument.audio.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.bot.indexDocument.audio.labels` | object | - |  |  |  |
| `spec.bot.indexDocument.docx` | object | - |  |  |  |
| `spec.bot.indexDocument.docx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.bot.indexDocument.docx.labels` | object | - |  |  |  |
| `spec.bot.indexDocument.image` | object | - |  |  |  |
| `spec.bot.indexDocument.image.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.bot.indexDocument.image.labels` | object | - |  |  |  |
| `spec.bot.indexDocument.pdf` | object | - |  |  |  |
| `spec.bot.indexDocument.pdf.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.bot.indexDocument.pdf.labels` | object | - |  |  |  |
| `spec.bot.indexDocument.pdf.processByModel` | boolean | - |  |  |  |
| `spec.bot.indexDocument.pptx` | object | - |  |  |  |
| `spec.bot.indexDocument.pptx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.bot.indexDocument.pptx.labels` | object | - |  |  |  |
| `spec.bot.indexDocument.video` | object | - |  |  |  |
| `spec.bot.indexDocument.video.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.bot.indexDocument.video.labels` | object | - |  |  |  |
| `spec.bot.indexMessage` | object | - |  |  |  |
| `spec.bot.indexMessage.includeBot` | boolean | **required** |  |  |  |
| `spec.bot.indexMessage.includeUser` | boolean | **required** |  |  |  |
| `spec.bot.indexMessage.minLength` | integer | **required** |  | format `int32` |  |
| `spec.database` | object | - |  |  |  |
| `spec.database.batchSize` | integer | **required** |  | format `int32` |  |
| `spec.database.columns` | array | **required** |  |  |  |
| `spec.database.columns[].indexDocumentUrl` | object | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.audio` | object | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.audio.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.database.columns[].indexDocumentUrl.audio.labels` | object | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.documentClass` | string | **required** |  | one of `pdf`, `docx`, `pptx`, `audio`, `video`, `image` |  |
| `spec.database.columns[].indexDocumentUrl.docx` | object | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.docx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.database.columns[].indexDocumentUrl.docx.labels` | object | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.image` | object | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.image.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.database.columns[].indexDocumentUrl.image.labels` | object | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.linkageType` | string | **required** |  | one of `as-source`, `as-destination` |  |
| `spec.database.columns[].indexDocumentUrl.pdf` | object | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.pdf.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.database.columns[].indexDocumentUrl.pdf.labels` | object | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.pdf.processByModel` | boolean | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.pptx` | object | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.pptx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.database.columns[].indexDocumentUrl.pptx.labels` | object | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.video` | object | - |  |  |  |
| `spec.database.columns[].indexDocumentUrl.video.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.database.columns[].indexDocumentUrl.video.labels` | object | - |  |  |  |
| `spec.database.columns[].isIdentifier` | boolean | - |  |  |  |
| `spec.database.columns[].isMaxValueColumn` | boolean | - |  |  |  |
| `spec.database.columns[].name` | string | **required** |  | matches `^[a-zA-Z_][a-zA-Z0-9_]*$` |  |
| `spec.database.dataConnectorName` | string | **required** |  |  |  |
| `spec.database.query` | string | **required** |  |  |  |
| `spec.googleDrive` | object | - |  |  |  |
| `spec.googleDrive.folderId` | string | **required** |  |  |  |
| `spec.googleDrive.indexDocument` | object | - |  |  |  |
| `spec.googleDrive.indexDocument.audio` | object | - |  |  |  |
| `spec.googleDrive.indexDocument.audio.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.googleDrive.indexDocument.audio.labels` | object | - |  |  |  |
| `spec.googleDrive.indexDocument.docx` | object | - |  |  |  |
| `spec.googleDrive.indexDocument.docx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.googleDrive.indexDocument.docx.labels` | object | - |  |  |  |
| `spec.googleDrive.indexDocument.image` | object | - |  |  |  |
| `spec.googleDrive.indexDocument.image.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.googleDrive.indexDocument.image.labels` | object | - |  |  |  |
| `spec.googleDrive.indexDocument.pdf` | object | - |  |  |  |
| `spec.googleDrive.indexDocument.pdf.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.googleDrive.indexDocument.pdf.labels` | object | - |  |  |  |
| `spec.googleDrive.indexDocument.pdf.processByModel` | boolean | - |  |  |  |
| `spec.googleDrive.indexDocument.pptx` | object | - |  |  |  |
| `spec.googleDrive.indexDocument.pptx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.googleDrive.indexDocument.pptx.labels` | object | - |  |  |  |
| `spec.googleDrive.indexDocument.video` | object | - |  |  |  |
| `spec.googleDrive.indexDocument.video.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.googleDrive.indexDocument.video.labels` | object | - |  |  |  |
| `spec.googleDrive.oAuthCredentialName` | string | **required** |  |  |  |
| `spec.googleDrive.recursive` | boolean | - |  |  |  |
| `spec.knowledgeBaseName` | string | **required** |  |  |  |
| `spec.loaderClass` | string | **required** |  | one of `web`, `database`, `bot`, `google-drive`, `onedrive` |  |
| `spec.oneDrive` | object | - |  |  |  |
| `spec.oneDrive.folderId` | string | - |  |  |  |
| `spec.oneDrive.folderPath` | string | - |  |  |  |
| `spec.oneDrive.indexDocument` | object | - |  |  |  |
| `spec.oneDrive.indexDocument.audio` | object | - |  |  |  |
| `spec.oneDrive.indexDocument.audio.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.oneDrive.indexDocument.audio.labels` | object | - |  |  |  |
| `spec.oneDrive.indexDocument.docx` | object | - |  |  |  |
| `spec.oneDrive.indexDocument.docx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.oneDrive.indexDocument.docx.labels` | object | - |  |  |  |
| `spec.oneDrive.indexDocument.image` | object | - |  |  |  |
| `spec.oneDrive.indexDocument.image.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.oneDrive.indexDocument.image.labels` | object | - |  |  |  |
| `spec.oneDrive.indexDocument.pdf` | object | - |  |  |  |
| `spec.oneDrive.indexDocument.pdf.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.oneDrive.indexDocument.pdf.labels` | object | - |  |  |  |
| `spec.oneDrive.indexDocument.pdf.processByModel` | boolean | - |  |  |  |
| `spec.oneDrive.indexDocument.pptx` | object | - |  |  |  |
| `spec.oneDrive.indexDocument.pptx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.oneDrive.indexDocument.pptx.labels` | object | - |  |  |  |
| `spec.oneDrive.indexDocument.video` | object | - |  |  |  |
| `spec.oneDrive.indexDocument.video.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.oneDrive.indexDocument.video.labels` | object | - |  |  |  |
| `spec.oneDrive.oAuthCredentialName` | string | **required** |  |  |  |
| `spec.oneDrive.recursive` | boolean | - |  |  |  |
| `spec.schedule` | string | **required** |  |  |  |
| `spec.timeZone` | string | **required** |  |  |  |
| `spec.web` | object | - |  |  |  |
| `spec.web.delayMs` | integer | - |  | format `int64` |  |
| `spec.web.limitPerUrl` | integer | - |  | format `int64` |  |
| `spec.web.maxDepth` | integer | - |  | format `int64` |  |
| `spec.web.siteMapUrl` | string | - |  |  |  |
| `spec.web.timeoutMs` | integer | **required** |  | format `int64` |  |
| `spec.web.urls` | array | - |  |  |  |
| `spec.web.waitForMs` | integer | **required** |  | format `int64` |  |
