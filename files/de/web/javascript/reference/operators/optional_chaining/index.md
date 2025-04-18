---
title: Optionales Chaining (?.)
slug: Web/JavaScript/Reference/Operators/Optional_chaining
l10n:
  sourceCommit: 9963311ecc877c0b78d9d7b65d054d67fb0fa39e
---

{{jsSidebar("Operators")}}

Der **optionale Chaining-Operator (`?.`)** greift auf eine Eigenschaft eines Objekts zu oder ruft eine Funktion auf. Wenn das Objekt, auf das zugegriffen wird, oder die Funktion, die mit diesem Operator aufgerufen wird, {{jsxref("undefined")}} oder [`null`](/de/docs/Web/JavaScript/Reference/Operators/null) ist, wird der Ausdruck abgebrochen und zu {{jsxref("undefined")}} ausgewertet, anstatt einen Fehler auszulösen.

{{InteractiveExample("JavaScript Demo: Optionales Chaining (?.) Operator", "taller")}}

```js interactive-example
const adventurer = {
  name: "Alice",
  cat: {
    name: "Dinah",
  },
};

const dogName = adventurer.dog?.name;
console.log(dogName);
// Expected output: undefined

console.log(adventurer.someNonExistentMethod?.());
// Expected output: undefined
```

## Syntax

```js-nolint
obj?.prop
obj?.[expr]
func?.(args)
```

## Beschreibung

Der Operator `?.` ähnelt dem Chaining-Operator `.`, mit dem Unterschied, dass der Ausdruck, anstatt einen Fehler zu verursachen, wenn eine Referenz {{Glossary("Nullish", "nullish")}} ([`null`](/de/docs/Web/JavaScript/Reference/Operators/null) oder {{jsxref("undefined")}}) ist, mit einem Rückgabewert von `undefined` abgebrochen wird. Bei Funktionsaufrufen gibt er `undefined` zurück, wenn die gegebene Funktion nicht existiert.

Dies führt zu kürzeren und einfacheren Ausdrücken beim Zugriff auf verkettete Eigenschaften, wenn die Möglichkeit besteht, dass eine Referenz fehlt. Es kann auch hilfreich sein, den Inhalt eines Objekts zu erkunden, wenn keine bekannte Garantie darüber besteht, welche Eigenschaften erforderlich sind.

Betrachten Sie zum Beispiel ein Objekt `obj`, das eine verschachtelte Struktur hat. Ohne optionales Chaining erfordert das Nachschlagen einer tief verschachtelten Sub-Eigenschaft die Validierung der Zwischenschritte der Referenzen, wie zum Beispiel:

```js
const nestedProp = obj.first && obj.first.second;
```

Der Wert von `obj.first` wird bestätigt, dass er nicht `null` (und nicht `undefined`) ist, bevor auf den Wert von `obj.first.second` zugegriffen wird. Dies verhindert den Fehler, der auftreten würde, wenn Sie `obj.first.second` direkt ohne Prüfung von `obj.first` zugreifen würden.

Dies ist ein idiomatisches Muster in JavaScript, aber es wird umständlich, wenn die Kette lang ist, und es ist nicht sicher. Zum Beispiel, wenn `obj.first` ein {{Glossary("Falsy", "Falsy")}} Wert ist, der nicht `null` oder `undefined` ist, wie `0`, würde es immer noch zum Abbruch führen und `nestedProp` zu `0` machen, was möglicherweise nicht wünschenswert ist.

Mit dem optionalen Chaining-Operator (`?.`) müssen Sie jedoch nicht explizit testen und auf den Zustand von `obj.first` abkürzen, bevor Sie versuchen, auf `obj.first.second` zuzugreifen:

```js
const nestedProp = obj.first?.second;
```

Durch die Verwendung des Operators `?.` anstelle von nur `.`, prüft JavaScript implizit, ob `obj.first` nicht `null` oder `undefined` ist, bevor versucht wird, auf `obj.first.second` zuzugreifen. Wenn `obj.first` `null` oder `undefined` ist, wird der Ausdruck automatisch abgebrochen und `undefined` zurückgegeben.

Dies entspricht dem Folgenden, außer dass die temporäre Variable tatsächlich nicht erstellt wird:

```js
const temp = obj.first;
const nestedProp =
  temp === null || temp === undefined ? undefined : temp.second;
```

Optionales Chaining kann nicht auf einem nicht deklarierten Stammobjekt verwendet werden, aber es kann mit einem Stammobjekt mit dem Wert `undefined` verwendet werden.

```js example-bad
undeclaredVar?.prop; // ReferenceError: undeclaredVar is not defined
```

### Optionales Chaining mit Funktionsaufrufen

Sie können optionales Chaining verwenden, wenn Sie versuchen, eine Methode aufzurufen, die möglicherweise nicht existiert. Dies kann hilfreich sein, etwa beim Verwenden einer API, bei der eine Methode möglicherweise nicht verfügbar ist, entweder aufgrund des Alters der Implementierung oder aufgrund einer Funktion, die auf dem Gerät des Benutzers nicht verfügbar ist.

Die Verwendung von optionalem Chaining mit Funktionsaufrufen bewirkt, dass der Ausdruck automatisch `undefined` zurückgibt, anstatt eine Ausnahme auszulösen, wenn die Methode nicht gefunden wird:

```js
const result = someInterface.customMethod?.();
```

Wenn es jedoch eine Eigenschaft mit einem solchen Namen gibt, die keine Funktion ist, wird die Verwendung von `?.` dennoch eine {{jsxref("TypeError")}}-Ausnahme auslösen: "someInterface.customMethod is not a function".

> [!NOTE]
> Wenn `someInterface` selbst `null` oder `undefined` ist, wird weiterhin eine {{jsxref("TypeError")}}-Ausnahme ausgelöst ("someInterface is null"). Wenn Sie erwarten, dass `someInterface` selbst `null` oder `undefined` sein kann, müssen Sie `?.` an dieser Position ebenfalls verwenden: `someInterface?.customMethod?.()`.

`eval?.()` ist der kürzeste Weg, um in den [_indirect eval_](/de/docs/Web/JavaScript/Reference/Global_Objects/eval#direct_and_indirect_eval) Modus zu gelangen.

### Optionales Chaining mit Ausdrücken

Sie können den optionalen Chaining-Operator auch mit der [Bracket-Notation](/de/docs/Web/JavaScript/Reference/Operators/Property_accessors#bracket_notation) verwenden, die es ermöglicht, einen Ausdruck als Eigenschaftsnamen zu übergeben:

```js
const nestedProp = obj?.["prop" + "Name"];
```

Dies ist besonders nützlich für Arrays, da Array-Indizes mit eckigen Klammern angesprochen werden müssen.

```js
function printMagicIndex(arr) {
  console.log(arr?.[42]);
}

printMagicIndex([0, 1, 2, 3, 4, 5]); // undefined
printMagicIndex(); // undefined; if not using ?., this would throw an error: "Cannot read properties of undefined (reading '42')"
```

### Ungültiges optionales Chaining

Es ist ungültig, das Ergebnis eines optionalen Chaining-Ausdrucks zuzuweisen:

```js-nolint example-bad
const object = {};
object?.property = 1; // SyntaxError: Invalid left-hand side in assignment
```

[Template-Literal-Tags](/de/docs/Web/JavaScript/Reference/Template_literals#tagged_templates) können keine optionale Kette sein (siehe [SyntaxError: tagged template cannot be used with optional chain](/de/docs/Web/JavaScript/Reference/Errors/Bad_optional_template)):

```js-nolint example-bad
String?.raw`Hello, world!`;
String.raw?.`Hello, world!`; // SyntaxError: Invalid tagged template on optional chain
```

Der Konstruktor von {{jsxref("Operators/new", "new")}} Ausdrücken kann keine optionale Kette sein (siehe [SyntaxError: new keyword cannot be used with an optional chain](/de/docs/Web/JavaScript/Reference/Errors/Bad_new_optional)):

```js-nolint example-bad
new Intl?.DateTimeFormat(); // SyntaxError: Invalid optional chain from new expression
new Map?.();
```

### Kurzschluss

Wenn Sie optionales Chaining mit Ausdrücken verwenden, wird der Ausdruck nicht ausgewertet, wenn der linke Operand `null` oder `undefined` ist. Zum Beispiel:

```js
const potentiallyNullObj = null;
let x = 0;
const prop = potentiallyNullObj?.[x++];

console.log(x); // 0 as x was not incremented
```

Nachfolgende Eigenschaftszugriffe werden ebenfalls nicht ausgewertet.

```js
const potentiallyNullObj = null;
const prop = potentiallyNullObj?.a.b;
// This does not throw, because evaluation has already stopped at
// the first optional chain
```

Dies entspricht:

```js
const potentiallyNullObj = null;
const prop =
  potentiallyNullObj === null || potentiallyNullObj === undefined
    ? undefined
    : potentiallyNullObj.a.b;
```

Dieses Kurzschlussverhalten tritt jedoch nur entlang einer kontinuierlichen "Kette" von Eigenschaftszugriffen auf. Wenn Sie einen Teil der Kette [gruppieren](/de/docs/Web/JavaScript/Reference/Operators/Grouping), werden nachfolgende Eigenschaftszugriffe dennoch ausgewertet.

```js
const potentiallyNullObj = null;
const prop = (potentiallyNullObj?.a).b;
// TypeError: Cannot read properties of undefined (reading 'b')
```

Dies entspricht:

```js
const potentiallyNullObj = null;
const temp = potentiallyNullObj?.a;
const prop = temp.b;
```

Außer dass die `temp` Variable nicht erstellt wird.

## Beispiele

### Einfaches Beispiel

Dieses Beispiel sucht nach dem Wert der Eigenschaft `name` für das Mitglied `CSS` in einer Map, wenn es kein solches Mitglied gibt. Das Ergebnis ist daher `undefined`.

```js
const myMap = new Map();
myMap.set("JS", { name: "Josh", desc: "I maintain things" });

const nameBar = myMap.get("CSS")?.name;
```

### Umgang mit optionalen Rückrufen oder Ereignis-Handlern

Wenn Sie Rückrufe oder Abrufmethoden aus einem Objekt mit einem [Destrukturierungsmuster](/de/docs/Web/JavaScript/Reference/Operators/Destructuring#object_destructuring) verwenden, können Sie nicht existierende Werte haben, die Sie nicht als Funktionen aufrufen können, es sei denn, Sie haben deren Existenz getestet. Mit `?.` können Sie diesen zusätzlichen Test vermeiden:

```js
// Code written without optional chaining
function doSomething(onContent, onError) {
  try {
    // Do something with the data
  } catch (err) {
    // Testing if onError really exists
    if (onError) {
      onError(err.message);
    }
  }
}
```

```js
// Using optional chaining with function calls
function doSomething(onContent, onError) {
  try {
    // Do something with the data
  } catch (err) {
    onError?.(err.message); // No exception if onError is undefined
  }
}
```

### Stapeln des optionalen Chaining-Operators

Mit verschachtelten Strukturen ist es möglich, optionales Chaining mehrfach zu verwenden:

```js
const customer = {
  name: "Carl",
  details: {
    age: 82,
    location: "Paradise Falls", // Detailed address is unknown
  },
};
const customerCity = customer.details?.address?.city;

// This also works with optional chaining function call
const customerName = customer.name?.getName?.(); // Method does not exist, customerName is undefined
```

### Kombination mit dem Nullish Coalescing Operator

Der [Nullish Coalescing Operator](/de/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing) kann nach dem optionalen Chaining verwendet werden, um einen Standardwert zu erstellen, wenn kein Wert gefunden wurde:

```js
function printCustomerCity(customer) {
  const customerCity = customer?.city ?? "Unknown city";
  console.log(customerCity);
}

printCustomerCity({
  name: "Nathan",
  city: "Paris",
}); // "Paris"
printCustomerCity({
  name: "Carl",
  details: { age: 82 },
}); // "Unknown city"
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Nullish Coalescing Operator (`??`)](/de/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing)
