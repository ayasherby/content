---
title: 'HTMLCanvasElement: webglcontextlost event'
slug: Web/API/HTMLCanvasElement/webglcontextlost_event
page-type: web-api-event
tags:
  - Event
  - Reference
  - WebGL
browser-compat: api.HTMLCanvasElement.webglcontextlost_event
---
{{APIRef}}

The **`webglcontextlost`** event of the [WebGL API](/en-US/docs/Web/API/WebGL_API) is fired if the user agent detects that the drawing buffer associated with a {{domxref("WebGLRenderingContext")}} object has been lost.

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">Bubbles</th>
      <td>No</td>
    </tr>
    <tr>
      <th scope="row">Cancelable</th>
      <td>Yes</td>
    </tr>
    <tr>
      <th scope="row">Interface</th>
      <td>{{domxref("WebGLContextEvent")}}</td>
    </tr>
    <tr>
      <th scope="row">Event handler property</th>
      <td>none</td>
    </tr>
  </tbody>
</table>

## Example

With the help of the {{domxref("WEBGL_lose_context")}} extension, you can simulate the `webglcontextlost` event:

```js
const canvas = document.getElementById('canvas');
const gl = canvas.getContext('webgl');

canvas.addEventListener('webglcontextlost', (event) => {
  console.log(event);
});

gl.getExtension('WEBGL_lose_context').loseContext();

// "webglcontextlost" event is logged.
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{domxref("WebGLContextEvent")}}
- {{domxref("WebGLRenderingContext.isContextLost()")}}
- {{domxref("WEBGL_lose_context")}}, {{domxref("WEBGL_lose_context.loseContext()")}}, {{domxref("WEBGL_lose_context.restoreContext()")}}
