---
title: "ValidityState: Eigenschaft `valid`"
short-title: valid
slug: Web/API/ValidityState/valid
l10n:
  sourceCommit: e9b6cd1b7fa8612257b72b2a85a96dd7d45c0200
---

{{APIRef("HTML DOM")}}

Die schreibgeschützte **`valid`**-Eigenschaft der [`ValidityState`](/de/docs/Web/API/ValidityState)-Schnittstelle gibt an, ob der Wert eines {{HTMLElement("input")}}-Elements alle Validierungsanforderungen erfüllt und daher als gültig angesehen wird.

Wenn `true`, entspricht das Element der {{cssxref(":valid")}} CSS-Pseudoklasse; ansonsten gilt die {{cssxref(":invalid")}} CSS-Pseudoklasse.

## Wert

Ein boolescher Wert, der `true` ist, wenn der `ValidityState` allen Anforderungen entspricht.

## Beispiele

### Anzeige des Gültigkeitszustands

Das folgende Beispiel überprüft die Gültigkeit eines [numerischen Eingabeelements](/de/docs/Web/HTML/Reference/Elements/input/number).
Eine Einschränkung wurde mit dem [`min`-Attribut](/de/docs/Web/HTML/Reference/Elements/input/number#min) hinzugefügt, das einen Mindestwert von `18` für die Eingabe festlegt.
Wenn der Benutzer einen Wert eingibt, der keine Zahl größer als 17 ist, schlägt die Validierung der Einschränkung fehl und die Styles, die `input:invalid` entsprechen, werden angewendet.

```css
input:invalid {
  outline: red solid 3px;
}
input:valid {
  outline: palegreen solid 3px;
}
```

```css hidden
body {
  margin: 0.5rem;
}
pre {
  padding: 1rem;
  height: 2rem;
  background-color: lightgrey;
  outline: 1px solid grey;
}
```

```html
<pre id="log">Validation logged here...</pre>
<input type="number" id="age" min="18" required />
```

```js
const userInput = document.getElementById("age");
const logElement = document.getElementById("log");

function log(text) {
  logElement.innerText = text;
}

userInput.addEventListener("input", () => {
  userInput.reportValidity();
  if (userInput.validity.valid) {
    log("Input OK…");
  } else {
    log("Bad input detected…");
  }
});
```

{{EmbedLiveSample("displaying_validity_state", "100%", "140")}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- ValidityState [badInput](/de/docs/Web/API/ValidityState/badInput), [customError](/de/docs/Web/API/ValidityState/customError) Eigenschaften.
- [Einschränkungsvalidierung](/de/docs/Web/HTML/Guides/Constraint_validation)
- [Formulare: Datenformularvalidierung](/de/docs/Learn_web_development/Extensions/Forms/Form_validation)
