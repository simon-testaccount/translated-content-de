---
title: stroke-dasharray
slug: Web/SVG/Reference/Attribute/stroke-dasharray
l10n:
  sourceCommit: c2fd97474834e061404b992c8397d4ccc4439a71
---

Das **`stroke-dasharray`** Attribut ist ein Präsentationsattribut, das das Muster aus Strichen und Lücken definiert, das verwendet wird, um die Kontur der Form zu zeichnen.

> [!NOTE]
> Als Präsentationsattribut hat `stroke-dasharray` auch ein entsprechendes CSS-Eigenschaftspendant: {{cssxref("stroke-dasharray")}}. Wenn beide angegeben sind, hat die CSS-Eigenschaft Vorrang.

Sie können dieses Attribut mit den folgenden SVG-Elementen verwenden:

- {{SVGElement('circle')}}
- {{SVGElement('ellipse')}}
- {{SVGElement('path')}}
- {{SVGElement('line')}}
- {{SVGElement('polygon')}}
- {{SVGElement('polyline')}}
- {{SVGElement('rect')}}
- {{SVGElement('text')}}
- {{SVGElement('textPath')}}
- {{SVGElement('tref')}}
- {{SVGElement('tspan')}}

## Beispiel

```css hidden
html,
body,
svg {
  height: 100%;
}
```

```html
<svg viewBox="0 0 30 12" xmlns="http://www.w3.org/2000/svg">
  <style>
    line {
      stroke: black;
    }
  </style>
  <!-- No dashes nor gaps -->
  <line x1="0" y1="1" x2="30" y2="1" />

  <!-- Dashes and gaps of the same size -->
  <line x1="0" y1="3" x2="30" y2="3" stroke-dasharray="4" />

  <!-- Dashes and gaps of different sizes -->
  <line x1="0" y1="5" x2="30" y2="5" stroke-dasharray="4 1" />

  <!-- Dashes and gaps of various sizes with an odd number of values -->
  <line x1="0" y1="7" x2="30" y2="7" stroke-dasharray="4 1 2" />

  <!-- Dashes and gaps of various sizes with an even number of values -->
  <line x1="0" y1="9" x2="30" y2="9" stroke-dasharray="4 1 2 3" />

  <!-- Dashes starting with a gap -->
  <line x1="0" y1="11" x2="30" y2="11" stroke-dasharray="0 4 0" />
</svg>
```

{{EmbedLiveSample("Example", '100%', 150)}}

## Nutzungshinweise

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">Wert</th>
      <td><code>none</code> | <code>&#x3C;dasharray></code></td>
    </tr>
    <tr>
      <th scope="row">Standardwert</th>
      <td><code>none</code></td>
    </tr>
    <tr>
      <th scope="row">Animierbar</th>
      <td>Ja</td>
    </tr>
  </tbody>
</table>

- \<dasharray>

  - : Eine Liste von durch Kommas und/oder Leerzeichen getrennten [`<length>`](/de/docs/Web/SVG/Guides/Content_type#length)s und [`<percentage>`](/de/docs/Web/SVG/Guides/Content_type#percentage)s, die die Längen der abwechselnden Striche und Lücken angeben.

    Wenn eine ungerade Anzahl von Werten angegeben wird, wird die Liste der Werte wiederholt, um eine gerade Anzahl von Werten zu erhalten. So ist `5,3,2` gleichwertig mit `5,3,2,5,3,2`.

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- CSS {{cssxref("stroke-dasharray")}} Eigenschaft
