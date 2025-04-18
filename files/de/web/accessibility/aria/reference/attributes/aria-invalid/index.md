---
title: aria-invalid
slug: Web/Accessibility/ARIA/Reference/Attributes/aria-invalid
l10n:
  sourceCommit: e9b6cd1b7fa8612257b72b2a85a96dd7d45c0200
---

Der `aria-invalid` Zustand gibt an, dass der eingegebene Wert nicht dem vom Anwendung erwarteten Format entspricht.

## Beschreibung

Das `aria-invalid` Attribut wird verwendet, um anzuzeigen, dass der in ein Eingabefeld eingegebene Wert nicht dem Format oder Wert entspricht, das die Anwendung akzeptiert. Dies kann Formate wie E-Mail-Adressen oder Telefonnummern umfassen. `aria-invalid` kann auch verwendet werden, um darauf hinzuweisen, dass ein erforderliches Feld leer ist.

Das `aria-invalid` Attribut kann mit jedem typischen HTML-Formularelement verwendet werden und ist nicht auf Elemente beschränkt, denen eine ARIA-Rolle zugewiesen wurde.

Das Attribut sollte als Ergebnis eines Validierungsprozesses mit JavaScript gesetzt werden. Wenn ein Wert als ungültig oder außerhalb des Bereichs bestimmt wird, setzen Sie `aria-invalid="true"` **und** informieren Sie den Benutzer über den Fehler. Für eine bessere Benutzererfahrung geben Sie Vorschläge, wie der Fehler behoben werden kann. Setzen Sie `aria-invalid="true"` nicht auf leeren erforderlichen Elementen, bevor der Benutzer versucht, das Formular abzusenden. Sie könnten noch dabei sein, es auszufüllen.

> [!NOTE]
> Wenn `aria-invalid` in Verbindung mit dem `aria-required` Attribut verwendet wird, sollte `aria-invalid` nicht vor dem Absenden des Formulars auf "true" gesetzt werden - nur als Reaktion auf die Validierung.

Derzeit gibt es vier Werte: neben `true` und `false` haben wir `grammar`, das verwendet werden kann, wenn ein grammatikalischer Fehler erkannt wird, und `spelling` für Rechtschreibfehler. Wenn das Attribut nicht vorhanden ist oder sein Wert `false` ist oder sein Wert eine leere Zeichenfolge ist, gilt der Standardwert `false`. Jeder andere Wert wird so behandelt, als wäre `true` gesetzt.

### Native HTML-Validierung

HTML verfügt über eine native Formularvalidierung. Wenn ein Benutzer ein Formular mit einem fehlerhaften Steuerelement absendet, zeigt das erste Formularsteuerelement mit einem ungültigen Wert eine Fehlermeldung an, nativ.

Wenn ein [`required`](/de/docs/Web/HTML/Reference/Attributes/required) Attribut auf einem Formularsteuerelement vorhanden ist, das nicht ausgefüllt ist, wird das Formular nicht abgesendet, und eine Fehlermeldung erscheint mit der Aufforderung "Bitte füllen Sie dieses Feld aus" oder etwas Ähnlichem. Die Nachrichten für die native Validierung variieren je nach Browser und können nicht gestylt werden.

```html
<input type="number" step="2" min="0" max="100" required />
```

Wenn der Benutzer im obigen Beispiel einen Wert eingegeben hätte, der den Maximalwert überschreitet, unter dem Minimalwert liegt oder nicht dem Schrittwert entspricht, würde eine Fehlermeldung erscheinen. Hätte der Benutzer "3" eingegeben, wäre die native Fehlermeldung ähnlich wie "Bitte geben Sie einen gültigen Wert ein."

Wenn Sie eigene Skripte zur Formularvalidierung erstellen, stellen Sie sicher, dass `aria-invalid` auf ungültigen Formularsteuerelementen enthalten ist, zusammen mit Styling (Verwenden Sie den `[aria-invalid="true"]` Attributselektor) und Nachrichten (mit [`aria-errormessage`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-errormessage)), um Benutzern zu helfen, zu verstehen, wo der Fehler liegt und wie er behoben werden kann.

## Werte

- `grammar`
  - : Ein grammatikalischer Fehler wurde erkannt.
- `false` (Standard)
  - : Es wurden keine Fehler im Wert erkannt.
- `spelling`
  - : Ein Rechtschreibfehler wurde erkannt.
- `true`
  - : Der vom Benutzer eingegebene Wert hat die Validierung nicht bestanden.

Jeder Wert, der nicht in dieser Liste ist, wird als `true` behandelt.

## Beispiel

Der folgende Ausschnitt zeigt eine vereinfachte Version von zwei Formularfeldern mit einer an das Blur-Ereignis gebundenen Validierungsfunktion. Beachten Sie, dass es nicht zwingend erforderlich ist, das Attribut zum Eingang hinzuzufügen, da der Standardwert für `aria-invalid` `false` ist.

```html
<ul>
  <li>
    <label for="name">Full Name</label>
    <input
      type="text"
      name="name"
      id="name"
      aria-required="true"
      aria-invalid="false"
      onblur="checkValidity('name', ' ', 'Invalid name entered (requires both first and last name)');" />
  </li>
  <li>
    <label for="email">Email Address</label>
    <input
      type="email"
      name="email"
      id="email"
      aria-required="true"
      aria-invalid="false"
      onblur="checkValidity('email', '@', 'Invalid email address');" />
  </li>
</ul>
```

Beachten Sie, dass es nicht notwendig ist, die Felder sofort beim Verlassen zu validieren; die Anwendung könnte warten, bis das Formular übermittelt wird (auch wenn dies nicht unbedingt empfohlen wird).

Der folgende Ausschnitt zeigt eine Validierungsfunktion, die nur auf das Vorhandensein eines bestimmten Zeichens prüft (in der realen Welt wird die Validierung wahrscheinlich anspruchsvoller sein):

```js
function checkValidity(id, searchTerm, msg) {
  const elem = document.getElementById(id);
  if (elem.value.includes(searchTerm)) {
    elem.setAttribute("aria-invalid", "false");
    updateAlert();
  } else {
    elem.setAttribute("aria-invalid", "true");
    updateAlert(msg);
  }
}
```

Der folgende Ausschnitt zeigt die Alarmfunktionen, die die Fehlermeldung hinzufügen (oder entfernen):

```js
function updateAlert(msg) {
  const oldAlert = document.getElementById("alert");
  if (oldAlert) {
    oldAlert.remove();
  }

  if (msg) {
    const newAlert = document.createElement("div");
    newAlert.setAttribute("role", "alert");
    newAlert.setAttribute("id", "alert");
    const content = document.createTextNode(msg);
    newAlert.appendChild(content);
    document.body.appendChild(newAlert);
  }
}
```

Beachten Sie, dass der Alarm das ARIA-Rollenattribut auf [`alert`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/alert_role) gesetzt hat.

## Zugehörige Rollen

Verwendet in Rollen:

- [`application`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/application_role)
- [`checkbox`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/checkbox_role)
- [`combobox`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/combobox_role)
- [`gridcell`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/gridcell_role)
- [`listbox`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/listbox_role)
- [`radiogroup`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/radiogroup_role)
- [`slider`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/slider_role)
- [`spinbutton`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/spinbutton_role)
- [`textbox`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/textbox_role)
- [`tree`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/tree_role)

Geerbt in Rolle:

- [`columnheader`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/columnheader_role)
- [`rowheader`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/rowheader_role)
- [`searchbox`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/searchbox_role)
- [`switch`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/switch_role)
- [`treegrid`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/treegrid_role)

## Spezifikationen

{{Specifications}}

## Siehe auch

- [`aria-errormessage`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-errormessage)
- CSS {{CSSXRef(':valid')}} Pseudoklasse
- CSS {{CSSXRef(':invalid')}} Pseudoklasse
- [Formularvalidierung](/de/docs/Learn_web_development/Extensions/Forms/Form_validation) Tutorial
