---
title: "SVGPathElement: setPathData() Methode"
short-title: setPathData()
slug: Web/API/SVGPathElement/setPathData
l10n:
  sourceCommit: 49bbddc34034e59a63c0b2cda79e45c94ea9daa9
---

{{APIRef("SVG")}}{{SeeCompatTable}}

Die **`SVGPathElement.setPathData()`** Methode setzt die Sequenz von Pfadsegmenten als neue Pfaddaten.

## Syntax

```js-nolint
setPathData(pathData)
```

### Parameter

- `pathData`

  - : Ein Array von Pfadsegmenten.
    Jedes Pfadsegment ist ein Objekt mit den folgenden Eigenschaften:

    - `type`
      - : Ein [Pfadbefehl](/de/docs/Web/SVG/Reference/Attribute/d#path_commands).
        Wenn [`options.normalize`](/de/docs/Web/API/SVGPathElement/getPathData#normalize) wahr ist, wird dies einer der absoluten Befehle sein: `'M'`, `'L'`, `'C'` und `'Z'`.
    - `values`
      - : Ein Array oder Wert, der die Parameter für den entsprechenden Befehl enthält.

### Rückgabewert

Keiner ({{jsxref('undefined')}}).

## Beispiel

### Pfaddaten setzen

Betrachten Sie das folgende `<path>` Element, das ein Quadrat zeichnet:

```xml
<svg xmlns="http://www.w3.org/2000/svg" width="64" height="64">
  <path d="M0,0 h64 v64 h-64 z" />
</svg>
```

Der unten stehende Code verwendet die [`getPathData()`](/de/docs/Web/API/SVGPathElement/getPathData) Methode, um die normalisierten Pfaddaten als [absolute Befehle](/de/docs/Web/SVG/Reference/Attribute/d#path_commands) zurückzugeben.
Das Zurücksetzen der zurückgegebenen Daten auf das `<path>` Element mit der `setPathData()` Methode führt zu einem anderen Satz von Pfadbefehl im DOM:

```js
const svgPath = document.querySelector("path");
const pathData = path.getPathData({ normalize: true });

svgPath.setPathData(pathData);

// <path d="M 0 0 L 64 0 L 64 64 L 0 64 Z" />
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}
