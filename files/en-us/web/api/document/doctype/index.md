---
title: Document.doctype
slug: Web/API/Document/doctype
page-type: web-api-instance-property
tags:
  - API
  - DOM
  - Document
  - Property
  - Reference
browser-compat: api.Document.doctype
---
{{ApiRef("DOM")}}

Returns the Document Type Declaration (DTD) associated with current document. The
returned object implements the {{domxref("DocumentType")}} interface. Use
{{domxref("DOMImplementation.createDocumentType()")}} to create a
`DocumentType`.

- `doctype` is a read-only property.

## Value

A {{domxref("DocumentType")}} object.

## Examples

```js
var doctypeObj = document.doctype;

console.log(
  "doctypeObj.name: "           + doctypeObj.name            + "\n" +
  "doctypeObj.internalSubset: " + doctypeObj.internalSubset  + "\n" +
  "doctypeObj.publicId: "       + doctypeObj.publicId        + "\n" +
  "doctypeObj.systemId: "       + doctypeObj.systemId
);
```

## Notes

The property returns `null` if there is no DTD associated with the current
document.

DOM level 2 doesn't support editing the document type declaration.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}
