---
title: min-width
slug: Web/CSS/min-width
l10n:
  sourceCommit: 702cd9e4d2834e13aea345943efc8d0c03d92ec9
---

{{CSSRef}}

Die **`min-width`** [CSS](/de/docs/Web/CSS) Eigenschaft legt die Mindestbreite eines Elements fest. Sie verhindert, dass der [verwendete Wert](/de/docs/Web/CSS/CSS_cascade/Value_processing#used_value) der {{cssxref("width")}}-Eigenschaft kleiner wird als der Wert, der für `min-width` angegeben ist.

{{InteractiveExample("CSS Demo: min-width")}}

```css interactive-example-choice
min-width: 150px;
```

```css interactive-example-choice
min-width: 20em;
```

```css interactive-example-choice
min-width: 75%;
```

```css interactive-example-choice
min-width: 40ch;
```

```html interactive-example
<section class="default-example" id="default-example">
  <div class="transition-all" id="example-element">
    Change the minimum width.
  </div>
</section>
```

```css interactive-example
#example-element {
  display: flex;
  flex-direction: column;
  background-color: #5b6dcd;
  height: 80%;
  justify-content: center;
  color: #ffffff;
}
```

Die Breite des Elements wird auf den Wert von `min-width` gesetzt, wann immer `min-width` größer als {{Cssxref("max-width")}} oder {{Cssxref("width")}} ist.

## Syntax

```css
/* <length> value */
min-width: 3.5em;
min-width: anchor-size(width);
min-width: anchor-size(--myAnchor self-inline, 200%);

/* <percentage> value */
min-width: 10%;

/* Keyword values */
min-width: max-content;
min-width: min-content;
min-width: fit-content;
min-width: fit-content(20em);
min-width: stretch;

/* Global values */
min-width: inherit;
min-width: initial;
min-width: revert;
min-width: revert-layer;
min-width: unset;
```

### Werte

- {{cssxref("&lt;length&gt;")}}
  - : Definiert die `min-width` als absoluten Wert.
- {{cssxref("&lt;percentage&gt;")}}
  - : Definiert die `min-width` als Prozentsatz der Breite des enthaltenen Blocks.
- `auto`

  - : Der Standardwert. Die Quelle des automatischen Wertes für das angegebene Element hängt von seinem Anzeige-Wert ab. Für Blockboxen, Inline-Boxen, Inline-Blöcke und alle Tabelleneinheits-Boxen wird `auto` zu `0`.

    Für {{Glossary("Flex_Item", "Flex-Elemente")}} und Grid-Elemente ist der Mindestbreitenwert entweder die angegebene empfohlene Größe, wie der Wert der `width`-Eigenschaft, die übertragene Größe, berechnet, wenn das Element ein `aspect-ratio` hat und die Höhe eine festgelegte Größe ist, andernfalls wird die `min-content` Größe verwendet. Wenn das Flex- oder Grid-Element ein {{Glossary("scroll_container", "Scroll-Container")}} ist oder wenn ein Grid-Element mehr als eine flexible Spaltenbahn überspannt, ist die automatische Mindestgröße `0`.

- `max-content`
  - : Die von Natur aus bevorzugte `min-width`.
- `min-content`
  - : Die von Natur aus minimale `min-width`.
- `fit-content`
  - : Nutzt den verfügbaren Raum, aber nicht mehr als [`max-content`](/de/docs/Web/CSS/max-content), also `min(max-content, max(min-content, stretch))`.
- `fit-content({{cssxref("&lt;length-percentage&gt;")}})`
  - : Verwendet die `fit-content`-Formel mit dem verfügbaren Raum, der durch das angegebene Argument ersetzt wird, d.h. `min(max-content, max(min-content, argument))`.
- `stretch`

  - : Begrenzet die Mindestbreite der [margin box](/de/docs/Learn_web_development/Core/Styling_basics/Box_model#parts_of_a_box) des Elements auf die Breite seines [enthältenden Blocks](/de/docs/Web/CSS/CSS_display/Containing_block#identifying_the_containing_block). Es wird versucht, die Randbox so zu gestalten, dass sie den verfügbaren Raum im enthältenden Block füllt und so ähnlich wie `100%` wirkt, aber die resultierende Größe auf die Randbox und nicht auf die durch [box-sizing](/de/docs/Web/CSS/box-sizing) bestimmte Box anwendet.

    > [!NOTE]
    > Um Aliase zu überprüfen, die von Browsern für den `stretch`-Wert verwendet werden, und deren Implementierungsstatus, sehen Sie im Abschnitt [Browser-Kompatibilität](#browser-kompatibilität) nach.

## Formale Definition

{{cssinfo}}

## Formale Syntax

{{csssyntax}}

## Beispiele

### Mindestbreite eines Elements festlegen

```css
table {
  min-width: 75%;
}

form {
  min-width: 0;
}
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{Cssxref("max-width")}}
- {{Cssxref("width")}}
- {{cssxref("min-inline-size")}}
- {{cssxref("min-block-size")}}
- {{cssxref("box-sizing")}}
- [Einführung in das CSS-Basis-Boxmodell](/de/docs/Web/CSS/CSS_box_model/Introduction_to_the_CSS_box_model)
- [CSS-Boxmodell](/de/docs/Web/CSS/CSS_box_model) Modul
