# Source

`asgard-ai.com/v1alpha1`, kind `Source`, plural `sources`, namespaced.

| field | type | required | default | constraints | what it is |
|---|---|---|---|---|---|
| `spec` | object | **required** |  |  |  |
| `spec.audio` | object | - |  |  |  |
| `spec.audio.indexers` | object | **required** |  |  |  |
| `spec.audio.indexers.*.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.audio.indexers.*.labels` | object | - |  |  |  |
| `spec.csv` | object | - |  |  |  |
| `spec.csv.indexers` | object | **required** |  |  |  |
| `spec.csv.indexers.*.columns` | array | **required** |  |  |  |
| `spec.csv.indexers.*.columns[].index` | integer | **required** |  | format `int32` |  |
| `spec.csv.indexers.*.columns[].isIdentifier` | boolean | - |  |  |  |
| `spec.csv.indexers.*.columns[].key` | string | **required** |  | matches `^[a-zA-Z_][a-zA-Z_0-9$]*$` |  |
| `spec.csv.indexers.*.labels` | object | - |  |  |  |
| `spec.csv.indexers.*.skipHeader` | boolean | **required** |  |  |  |
| `spec.deletedIndexerKeys` | array | **required** |  |  |  |
| `spec.docx` | object | - |  |  |  |
| `spec.docx.indexers` | object | **required** |  |  |  |
| `spec.docx.indexers.*.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.docx.indexers.*.labels` | object | - |  |  |  |
| `spec.image` | object | - |  |  |  |
| `spec.image.indexers` | object | **required** |  |  |  |
| `spec.image.indexers.*.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.image.indexers.*.labels` | object | - |  |  |  |
| `spec.jsonLine` | object | - |  |  |  |
| `spec.jsonLine.indexers` | object | **required** |  |  |  |
| `spec.jsonLine.indexers.*.fields` | array | **required** |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.audio` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.audio.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.audio.labels` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.documentClass` | string | **required** |  | one of `pdf`, `docx`, `pptx`, `audio`, `video`, `image` |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.docx` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.docx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.docx.labels` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.image` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.image.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.image.labels` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.linkageType` | string | **required** |  | one of `as-source`, `as-destination` |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.pdf` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.pdf.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.pdf.labels` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.pdf.processByModel` | boolean | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.pptx` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.pptx.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.pptx.labels` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.video` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.video.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.jsonLine.indexers.*.fields[].indexDocumentUrl.video.labels` | object | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].isIdentifier` | boolean | - |  |  |  |
| `spec.jsonLine.indexers.*.fields[].jsonPath` | string | **required** |  |  |  |
| `spec.jsonLine.indexers.*.fields[].key` | string | **required** |  |  |  |
| `spec.jsonLine.indexers.*.labels` | object | - |  |  |  |
| `spec.knowledgeBaseName` | string | **required** |  |  |  |
| `spec.pdf` | object | - |  |  |  |
| `spec.pdf.indexers` | object | **required** |  |  |  |
| `spec.pdf.indexers.*.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.pdf.indexers.*.labels` | object | - |  |  |  |
| `spec.pdf.indexers.*.processByModel` | boolean | - |  |  |  |
| `spec.pptx` | object | - |  |  |  |
| `spec.pptx.indexers` | object | **required** |  |  |  |
| `spec.pptx.indexers.*.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.pptx.indexers.*.labels` | object | - |  |  |  |
| `spec.sourceClass` | string | **required** |  | one of `pdf`, `docx`, `pptx`, `audio`, `video`, `image`, `csv`, `xlsx`, `json-line` |  |
| `spec.video` | object | - |  |  |  |
| `spec.video.indexers` | object | **required** |  |  |  |
| `spec.video.indexers.*.chunkSize` | integer | **required** |  | format `int32` |  |
| `spec.video.indexers.*.labels` | object | - |  |  |  |
| `spec.xlsx` | object | - |  |  |  |
| `spec.xlsx.indexers` | object | **required** |  |  |  |
| `spec.xlsx.indexers.*.columns` | array | **required** |  |  |  |
| `spec.xlsx.indexers.*.columns[].isIdentifier` | boolean | - |  |  |  |
| `spec.xlsx.indexers.*.columns[].key` | string | **required** |  | matches `^[a-zA-Z_][a-zA-Z_0-9$]*$` |  |
| `spec.xlsx.indexers.*.columns[].name` | string | **required** |  | matches `^[A-Z]+$` |  |
| `spec.xlsx.indexers.*.labels` | object | - |  |  |  |
| `spec.xlsx.indexers.*.sheetName` | string | **required** |  |  |  |
| `spec.xlsx.indexers.*.skipHeader` | boolean | **required** |  |  |  |
