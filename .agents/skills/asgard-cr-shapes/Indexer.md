# Indexer

`asgard-ai.com/v1alpha1`, kind `Indexer`, plural `indexers`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.audio` | object | - |  |  |  |
| `spec.audio.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.audio.labels` | object | - |  |  |  |
| `spec.csv` | object | - |  |  |  |
| `spec.csv.columns` | array | **required** |  |  |  |
| `spec.csv.columns[].index` | integer | **required** |  | format `int32` |  |
| `spec.csv.columns[].isIdentifier` | boolean | - |  |  |  |
| `spec.csv.columns[].key` | string | **required** |  | matches `^[a-zA-Z_][a-zA-Z_0-9$]*$` |  |
| `spec.csv.labels` | object | - |  |  |  |
| `spec.csv.skipHeader` | boolean | **required** |  |  |  |
| `spec.docx` | object | - |  |  |  |
| `spec.docx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.docx.labels` | object | - |  |  |  |
| `spec.etag` | string | **required** |  |  |  |
| `spec.image` | object | - |  |  |  |
| `spec.image.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.image.labels` | object | - |  |  |  |
| `spec.jsonLine` | object | - |  |  |  |
| `spec.jsonLine.fields` | array | **required** |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl` | object | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.audio` | object | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.audio.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.jsonLine.fields[].indexDocumentUrl.audio.labels` | object | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.documentClass` | string | **required** |  | one of `pdf`, `docx`, `pptx`, `audio`, `video`, `image` |  |
| `spec.jsonLine.fields[].indexDocumentUrl.docx` | object | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.docx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.jsonLine.fields[].indexDocumentUrl.docx.labels` | object | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.image` | object | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.image.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.jsonLine.fields[].indexDocumentUrl.image.labels` | object | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.linkageType` | string | **required** |  | one of `as-source`, `as-destination` |  |
| `spec.jsonLine.fields[].indexDocumentUrl.pdf` | object | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.pdf.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.jsonLine.fields[].indexDocumentUrl.pdf.labels` | object | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.pdf.processByModel` | boolean | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.pptx` | object | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.pptx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.jsonLine.fields[].indexDocumentUrl.pptx.labels` | object | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.video` | object | - |  |  |  |
| `spec.jsonLine.fields[].indexDocumentUrl.video.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.jsonLine.fields[].indexDocumentUrl.video.labels` | object | - |  |  |  |
| `spec.jsonLine.fields[].isIdentifier` | boolean | - |  |  |  |
| `spec.jsonLine.fields[].jsonPath` | string | **required** |  |  |  |
| `spec.jsonLine.fields[].key` | string | **required** |  |  |  |
| `spec.jsonLine.labels` | object | - |  |  |  |
| `spec.pdf` | object | - |  |  |  |
| `spec.pdf.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.pdf.labels` | object | - |  |  |  |
| `spec.pdf.processByModel` | boolean | - |  |  |  |
| `spec.pptx` | object | - |  |  |  |
| `spec.pptx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.pptx.labels` | object | - |  |  |  |
| `spec.sinkKnowledgeBaseName` | string | **required** |  |  |  |
| `spec.sourceBlobKey` | string | **required** |  |  |  |
| `spec.sourceClass` | string | **required** |  | one of `pdf`, `docx`, `pptx`, `audio`, `video`, `image`, `csv`, `xlsx`, `json-line` |  |
| `spec.video` | object | - |  |  |  |
| `spec.video.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.video.labels` | object | - |  |  |  |
| `spec.xlsx` | object | - |  |  |  |
| `spec.xlsx.columns` | array | **required** |  |  |  |
| `spec.xlsx.columns[].isIdentifier` | boolean | - |  |  |  |
| `spec.xlsx.columns[].key` | string | **required** |  | matches `^[a-zA-Z_][a-zA-Z_0-9$]*$` |  |
| `spec.xlsx.columns[].name` | string | **required** |  | matches `^[A-Z]+$` |  |
| `spec.xlsx.labels` | object | - |  |  |  |
| `spec.xlsx.sheetName` | string | **required** |  |  |  |
| `spec.xlsx.skipHeader` | boolean | **required** |  |  |  |
