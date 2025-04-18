---
title: VisualViewport
slug: Web/API/VisualViewport
l10n:
  sourceCommit: 93b34fcdb9cf91ff44f5dfe7f4dcd13e961962da
---

{{APIRef("Visual Viewport")}}

Die **`VisualViewport`**-Schnittstelle der [Visual Viewport API](/de/docs/Web/API/Visual_Viewport_API) repräsentiert das visuelle Viewport für ein gegebenes Fenster. Für eine Seite mit iframes hat jedes iframe sowie die enthaltende Seite ein einzigartiges Fensterobjekt. Jedes Fenster auf einer Seite hat ein einzigartiges `VisualViewport`, das die mit diesem Fenster verbundenen Eigenschaften darstellt.

Sie können das visuelle Viewport eines Fensters mit [`Window.visualViewport`](/de/docs/Web/API/Window/visualViewport) abrufen.

> [!NOTE]
> Nur das oberste Fenster hat ein visuelles Viewport, das sich vom Layout-Viewport unterscheidet. Daher ist im Allgemeinen nur das `VisualViewport`-Objekt des obersten Fensters nützlich. Für ein {{htmlelement("iframe")}} entsprechen die metrischen Angaben des visuellen Viewports wie [`VisualViewport.width`](/de/docs/Web/API/VisualViewport/width) immer den metrischen Angaben des Layout-Viewports wie [`document.documentElement.clientWidth`](/de/docs/Web/API/Element/clientWidth).

{{InheritanceDiagram}}

## Instanz-Eigenschaften

_Erbt auch Eigenschaften von seiner übergeordneten Schnittstelle, [`EventTarget`](/de/docs/Web/API/EventTarget)._

- [`VisualViewport.offsetLeft`](/de/docs/Web/API/VisualViewport/offsetLeft) {{ReadOnlyInline}}
  - : Gibt den Versatz der linken Kante des visuellen Viewports von der linken Kante des Layout-Viewports in CSS-Pixeln zurück.
- [`VisualViewport.offsetTop`](/de/docs/Web/API/VisualViewport/offsetTop) {{ReadOnlyInline}}
  - : Gibt den Versatz der oberen Kante des visuellen Viewports von der oberen Kante des Layout-Viewports in CSS-Pixeln zurück.
- [`VisualViewport.pageLeft`](/de/docs/Web/API/VisualViewport/pageLeft) {{ReadOnlyInline}}
  - : Gibt die x-Koordinate des visuellen Viewports relativ zum Ursprung des initialen enthaltenden Blocks in CSS-Pixeln zurück.
- [`VisualViewport.pageTop`](/de/docs/Web/API/VisualViewport/pageTop) {{ReadOnlyInline}}
  - : Gibt die y-Koordinate des visuellen Viewports relativ zum Ursprung des initialen enthaltenden Blocks in CSS-Pixeln zurück.
- [`VisualViewport.width`](/de/docs/Web/API/VisualViewport/width) {{ReadOnlyInline}}
  - : Gibt die Breite des visuellen Viewports in CSS-Pixeln zurück.
- [`VisualViewport.height`](/de/docs/Web/API/VisualViewport/height) {{ReadOnlyInline}}
  - : Gibt die Höhe des visuellen Viewports in CSS-Pixeln zurück.
- [`VisualViewport.scale`](/de/docs/Web/API/VisualViewport/scale) {{ReadOnlyInline}}
  - : Gibt den Pinch-Zoom-Skalierungsfaktor zurück, der auf das visuelle Viewport angewendet wird.

## Instanz-Methoden

_Erbt auch Methoden von seiner übergeordneten Schnittstelle, [`EventTarget`](/de/docs/Web/API/EventTarget)._

## Ereignisse

Hören Sie auf diese Ereignisse mit [`addEventListener()`](/de/docs/Web/API/EventTarget/addEventListener) oder durch Zuweisen eines Ereignislisteners zur relevanten `oneventname`-Eigenschaft dieser Schnittstelle.

- [`resize`](/de/docs/Web/API/VisualViewport/resize_event)
  - : Wird ausgelöst, wenn das visuelle Viewport geändert wird.
    Ebenfalls verfügbar über die `onresize`-Eigenschaft.
- [`scroll`](/de/docs/Web/API/VisualViewport/scroll_event)
  - : Wird ausgelöst, wenn das visuelle Viewport gescrollt wird.
    Ebenfalls verfügbar über die `onscroll`-Eigenschaft.
- [`scrollend`](/de/docs/Web/API/VisualViewport/scrollend_event)
  - : Wird ausgelöst, wenn eine Scroll-Operation auf dem visuellen Viewport endet.
    Ebenfalls verfügbar über die `onscrollend`-Eigenschaft.

## Beispiele

### Verstecken eines überlagerten Kastens beim Zoomen

Dieses Beispiel, übernommen aus dem [Visual Viewport README](https://github.com/WICG/visual-viewport), zeigt, wie man etwas Code schreiben kann, der einen überlagerten Kasten (der beispielsweise eine Werbung enthalten könnte) ausblendet, wenn der Benutzer hineinzoomt. Dies ist eine gute Möglichkeit, die Benutzererfahrung beim Zoomen auf Seiten zu verbessern. Ein [Live-Beispiel](https://wicg.github.io/visual-viewport/examples/hide-on-zoom.html) ist ebenfalls verfügbar.

```js
const bottomBar = document.getElementById("bottom-bar");
const viewport = window.visualViewport;

function resizeHandler() {
  bottomBar.style.display = viewport.scale > 1.3 ? "none" : "block";
}

window.visualViewport.addEventListener("resize", resizeHandler);
```

### Simulieren von position: device-fixed

Dieses Beispiel, ebenfalls aus dem [Visual Viewport README](https://github.com/WICG/visual-viewport), zeigt, wie diese API verwendet werden kann, um `position: device-fixed` zu simulieren, welches Elemente am visuellen Viewport fixiert. Ein [Live-Beispiel](https://wicg.github.io/visual-viewport/examples/fixed-to-viewport.html) ist ebenfalls verfügbar.

```js
const bottomBar = document.getElementById("bottom-bar");
const viewport = window.visualViewport;
function viewportHandler() {
  const layoutViewport = document.getElementById("layoutViewport");

  // Since the bar is position: fixed we need to offset it by the visual
  // viewport's offset from the layout viewport origin.
  const offsetLeft = viewport.offsetLeft;
  const offsetTop =
    viewport.height -
    layoutViewport.getBoundingClientRect().height +
    viewport.offsetTop;

  // You could also do this by setting style.left and style.top if you
  // use width: 100% instead.
  bottomBar.style.transform = `translate(${offsetLeft}px, ${offsetTop}px) scale(${
    1 / viewport.scale
  })`;
}
window.visualViewport.addEventListener("scroll", viewportHandler);
window.visualViewport.addEventListener("resize", viewportHandler);
```

> [!NOTE]
> Diese Technik sollte mit Vorsicht verwendet werden; das Nachahmen von `position: device-fixed` auf diese Weise kann dazu führen, dass das fixierte Element beim Scrollen flackert.

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Web Viewports Erklärer](https://github.com/bokand/bokand.github.io/blob/master/web_viewports_explainer.md) — nützliche Erklärung von Web-Viewport-Konzepten, einschließlich des Unterschieds zwischen visuellem Viewport und Layout-Viewport.
