---
title: Symbol
slug: Web/JavaScript/Reference/Global_Objects/Symbol
l10n:
  sourceCommit: c40fe6508ac4add549d315aa20f6bc2fca49c27e
---

{{JSRef}}

**`Symbol`** — это встроенный объект, конструктор которого возвращает значение [примитивного типа](/ru/docs/Glossary/Primitive) `symbol`. Такие значения называют **символьными значениями** (**Symbol value**) или просто **символами** (**Symbol**), их основная особенность в том, что они гарантируют уникальность. Символы часто используются в качестве уникальных ключей объекта. Они не пересекаются с ключами, которые могут быть добавлены другим кодом, а также скрыты от доступа из другого кода. Это обеспечивает возможность слабой {{Glossary("encapsulation", "инкапсуляции")}} или слабую форму [сокрытия информации](<https://ru.wikipedia.org/wiki/Сокрытие_(программирование)>).

Каждый вызов `Symbol()` гарантированно возвращает уникальный символ. Каждый вызов `Symbol.for("key")` всегда будет возвращать один и тот же символ для указанного значения `"key"`. При вызове `Symbol.for("key")` осуществляется поиск в глобальном реестре символов. Если символ найден, то он возвращается, в противном случае создаётся новый символ, добавляется в глобальный реестр под заданным ключом и возвращается.

## Описание

Чтобы создать новое символьное значение, достаточно написать `Symbol()`, указав по желанию строку в качестве описания:

```js
const sym1 = Symbol();
const sym2 = Symbol("foo");
const sym3 = Symbol("foo");
```

Код выше создаёт три новых символа. Обратите внимание, что `Symbol("foo")` не выполняет приведение строки "foo" к символу. Это выражение создаёт каждый раз новый символ:

```js
Symbol("foo") === Symbol("foo"); // false
```

Код ниже с оператором {{jsxref("Operators/new", "new")}} вызовет исключение {{jsxref("TypeError")}}:

```js example-bad
const sym = new Symbol(); // TypeError
```

Это удерживает разработчиков от создания явного объекта-обёртки `Symbol` вместо нового символьного значения, но может быть неожиданным, так как создание явных объектов-обёрток для примитивных типов доступно (например, `new Boolean`, `new String`, `new Number`).

Если действительно необходимо обернуть символ в объект, можно использовать функцию `Object()`:

```js
const sym = Symbol("foo");
typeof sym; // "symbol"
const symObj = Object(sym);
typeof symObj; // "object"
```

Поскольку символы — единственный примитивный тип данных, который имеет ссылочную идентичность (то есть нельзя создать один и тот же символ дважды), они в некотором смысле ведут себя как объекты. Например, они подлежат возможности сборки мусора и поэтому могут храниться в {{jsxref("WeakMap")}}, {{jsxref("WeakSet")}}, {{jsxref("WeakRef")}} и {{jsxref("FinalizationRegistry")}}.

### Общие символы в глобальном реестре символов

Приведённый выше синтаксис использования функции `Symbol()` создаёт символ, значение которого будет уникальным на протяжении всего времени существования программы. Чтобы создавать символы, доступные в разных файлах и даже областях видимости, можно использовать методы {{jsxref("Symbol.for()")}} и {{jsxref("Symbol.keyFor()" )}} для установки и получения символов из глобального реестра символов.

Обратите внимание, что «глобальный реестр символов» — это всего лишь концепция. Реализация может не соответствовать какой-либо внутренней структуре данных в движке JavaScript, и даже если такой реестр существует, его содержимое недоступно для кода JavaScript, кроме как через методы `for()` и `keyFor()`.

Метод `Symbol.for(tokenString)` принимает строковый ключ и возвращает символьное значение из реестра, а метод `Symbol.keyFor(symbolValue)` принимает символьное значение и возвращает соответствующий ему строковый ключ. Каждый из них является обратным другому, поэтому следующее выражение истинно:

```js
Symbol.keyFor(Symbol.for("tokenString")) === "tokenString"; // true
```

Поскольку зарегистрированные символы могут быть созданы в произвольном месте, они ведут себя почти так же, как строки, которые они оборачивают, их уникальность не гарантируется они не подлежат возможности сборке мусора. Поэтому зарегистрированные символы нельзя использовать в {{jsxref("WeakMap")}}, {{jsxref("WeakSet")}}, {{jsxref("WeakRef")}} и {{jsxref("FinalizationRegistry")}}.

### Общеизвестные символы

Все статические свойства конструктора `Symbol` сами являются символами, значение которых одинаковы во всех областях видимости. Они называются _общеизвестными символами_ и служат «протоколами» для некоторых встроенных операций JavaScript, позволяя пользователям настраивать поведение языка. Например, если функция-конструктор имеет метод с именем {{jsxref("Symbol.hasInstance")}}, то его поведение будет реализовано с помощью оператора {{jsxref("Operators/instanceof", "instanceof")}}.

До появления общеизвестных символов в JavaScript использовались обычные свойства для реализации определённых встроенных операций. Например, функция [`JSON.stringify`](/ru/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) попытается вызвать метод объекта `toJSON()`, а функция [`String `](/ru/docs/Web/JavaScript/Reference/Global_Objects/String/String) вызовет методы объекта `toString()` и `valueOf()`. Однако по мере того, как в язык добавляется всё больше новых операций, назначение каждой операции «магического свойства» может нарушить обратную совместимость и затруднить понимание поведения языка. Общеизвестные символы позволяют настройкам быть «невидимыми» для обычного кода, который как правило обращается только к строковым свойствам.

В MDN и других источниках значения общеизвестных символов обозначаются с помощью префикса `@@`. Например, {{jsxref("Symbol.hasInstance")}} записывается как `@@hasInstance`. Это связано с тем, что символы не имеют фактических литеральных форматов, а использование `Symbol.hasInstance` не отражает возможность использования других псевдонимов для ссылки на тот же символ. Это похоже на разницу между `Function.name` и `Function`.

Общеизвестные символы не подлежат возможности сборки мусора, поскольку они входят в фиксированный набор и уникальны на протяжении всего времени существования программы, подобно внутренним объектам, таким как `Array.prototype`. Поэтому их также можно использовать в {{ jsxref("WeakMap")}}, {{jsxref("WeakSet")}}, {{jsxref("WeakRef")}} и {{jsxref("FinalizationRegistry")}}.

### Поиск символьных свойств у объектов

Метод {{jsxref("Object.getOwnPropertySymbols()")}} возвращает массив символов и позволяет получить символьные свойства конкретного объекта. Следует отметить, что при инициализации у объектов нет своих символьных свойств, поэтому этот массив будет пуст, пока у объекта не будут установлены символьные свойства.

## Конструктор

- {{jsxref("Symbol/Symbol", "Symbol()")}}
  - : Создаёт новый объект `Symbol`. Не является конструктором в привычном понимании, потому что может быть вызван только как обычная функция, но не `new Symbol()`.

## Статические свойства

Статические свойства являются общеизвестными символами. Для описания таких символов мы используем выражения подобные «`Symbol.hasInstance` — это метод, определяющий…», но следует иметь в виду, что это относится к семантике метода объекта, имеющего этот символ в качестве имени метода (поскольку общеизвестные символы действуют как «протоколы»), а не описывает значение самого символа.

- {{jsxref("Symbol.asyncIterator")}}
  - : Метод возвращает используемый по умолчанию AsyncIterator объекта. Используется в [`for await...of`](/ru/docs/Web/JavaScript/Reference/Statements/for-await...of).
- {{jsxref("Symbol.hasInstance")}}
  - : Метод определяет, распознаёт ли конструктор объект как свой экземпляр. Используется в {{jsxref("Operators/instanceof", "instanceof")}}.
- {{jsxref("Symbol.isConcatSpreadable")}}
  - : Логическое значение, указывающее, может ли объект быть сведён к элементам массива. Используется в {{jsxref("Array.prototype.concat()")}}.
- {{jsxref("Symbol.iterator")}}
  - : Метод возвращает используемый по умолчанию итератор объекта. Используется в [`for...of`](/ru/docs/Web/JavaScript/Reference/Statements/for...of).
- {{jsxref("Symbol.match")}}
  - : Метод для сопоставления со строкой, также используется для определения того, можно ли использовать объект в качестве регулярного выражения. Используется в {{jsxref("String.prototype.match()")}}.
- {{jsxref("Symbol.matchAll")}}
  - : Метод возвращает итератор, который определяет совпадения строки с регулярным выражением. Используется в {{jsxref("String.prototype.matchAll()")}}.
- {{jsxref("Symbol.replace")}}
  - : Метода заменяет совпадающие подстроки в строке. Используется в {{jsxref("String.prototype.replace()")}}.
- {{jsxref("Symbol.search")}}
  - : Метод, возвращающий индекс внутри строки, соответствующий регулярному выражению. Используется в {{jsxref("String.prototype.search()")}}.
- {{jsxref("Symbol.species")}}
  - : Функция-конструктор, используемая для создания производных объектов.
- {{jsxref("Symbol.split")}}
  - : Метод, который разбивает строку по индексам, соответствующим регулярному выражению. Используется в {{jsxref("String.prototype.split()")}}.
- {{jsxref("Symbol.toPrimitive")}}
  - : Метод преобразует объект в примитивное значение.
- {{jsxref("Symbol.toStringTag")}}
  - : Строковое значение, используемое для описания объекта по умолчанию. Используется в {{jsxref("Object.prototype.toString()")}}.
- {{jsxref("Symbol.unscopables")}}
  - : Значение объекта, имена собственных и унаследованных свойств которого исключены из привязок [`with`](/ru/docs/Web/JavaScript/Reference/Statements/with) связанного объекта.

## Статические методы

- {{jsxref("Symbol.for()")}}
  - : Ищет существующие зарегистрированные символы в глобальном реестре символов с указанным ключом и возвращает его, если он найден. В противном случае будет создан новый символ и зарегистрирован с указанным ключом.
- {{jsxref("Symbol.keyFor()")}}
  - : Извлекает общий ключ символа из глобального реестра символов для данного символа.

## Свойства экземпляра

Эти свойства определены в `Symbol.prototype` и есть у всех экземпляров `Symbol`.

- {{jsxref("Object/constructor", "Symbol.prototype.constructor")}}
  - : Функция-конструктор, создающая экземпляр объекта. Для экземпляров `Symbol` начальным значением является конструктор {{jsxref("Symbol/Symbol", "Symbol")}}.
- {{jsxref("Symbol.prototype.description")}}
  - : Доступная только для чтения строка с описанием символа.
- `Symbol.prototype[@@toStringTag]`
  - : Начальным значением свойства [`@@toStringTag`](/ru/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toStringTag) является строка `"Symbol"`. Это свойство используется в {{jsxref("Object.prototype.toString()")}}. Однако из-за того, что у `Symbol` есть свой собственный метод [`toString()`](/ru/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toString), это свойство не используется если не будет вызван [`Object.prototype.toString.call()`](/ru/docs/Web/JavaScript/Reference/Global_Objects/Function/call) с символом `thisArg`.

## Методы экземпляра

- {{jsxref("Symbol.prototype.toString()")}}
  - : Возвращает строку с описанием символа. Переопределяет метод {{jsxref("Object.prototype.toString()")}}.
- {{jsxref("Symbol.prototype.valueOf()")}}
  - : Возвращает символ. Переопределяет метод {{jsxref("Object.prototype.valueOf()")}}.
- [`Symbol.prototype[@@toPrimitive]()`](/ru/docs/Web/JavaScript/Reference/Global_Objects/Symbol/@@toPrimitive)
  - : Возвращает символ.

## Примеры

### Использование оператора `typeof` с символами

Оператор {{jsxref("Operators/typeof", "typeof")}} позволяет определять символы.

```js
typeof Symbol() === "symbol";
typeof Symbol("foo") === "symbol";
typeof Symbol.iterator === "symbol";
```

### Преобразование типов с символами

При преобразовании символов необходимо учитывать следующее.

- При попытке конвертировать символ в число возникает исключение {{jsxref("TypeError")}} (например, `+sym` или `sym | 0`).
- Результатом нестрогого сравнения `Object(sym) == sym` будет `true`.
- `Symbol("foo") + "bar"` вызывает исключение {{jsxref("TypeError")}} (невозможно преобразовать символ в строку). Это помогает избежать случайного создания строкового свойства объекта из символа.
- Более ["безопасный" вызов `String(sym)`](/ru/docs/Web/JavaScript/Reference/Global_Objects/String#String_conversion) работает с символами как вызов {{jsxref("Symbol.prototype.toString()")}}. Обратите внимание, что в то же время `new String(sym)` вызовет исключение.

### Символы и конструкция `for...in`

Символы не перечисляются при итерации [`for...in`](/ru/docs/Web/JavaScript/Reference/Statements/for...in). В дополнение к этому, {{jsxref("Object.getOwnPropertyNames()")}} не вернёт свойства символьного объекта. Тем не менее, их можно получить с помощью {{jsxref("Object.getOwnPropertySymbols()")}}.

```js
const obj = {};

obj[Symbol("a")] = "a";
obj[Symbol.for("b")] = "b";
obj["c"] = "c";
obj.d = "d";

for (const i in obj) {
  console.log(i);
}
// "c" "d"
```

### Символы и `JSON.stringify()`

При использовании `JSON.stringify()` полностью игнорируются свойства с символьными ключами:

```js
JSON.stringify({ [Symbol("foo")]: "foo" }); // '{}'
```

Более подробная информация в {{jsxref("JSON.stringify()")}}.

### Объекты-обёртки для символов в качестве ключей свойств

Когда объект-обёртка символа используется в качестве ключа свойства, этот объект приводится к символу, который он оборачивает:

```js
const sym = Symbol("foo");
const obj = { [sym]: 1 };
obj[sym]; // 1
obj[Object(sym)]; // тоже 1
```

## Спецификации

{{Specifications}}

## Совместимость с браузерами

{{Compat}}

## Смотрите также

- [Полифил `Symbol` в `core-js`](https://github.com/zloirock/core-js#ecmascript-symbol)
- {{jsxref("Operators/typeof", "typeof")}}
- [Типы и структуры данных JavaScript](/ru/docs/Web/JavaScript/Data_structures)
- [ES6 In Depth: Symbols](https://hacks.mozilla.org/2015/06/es6-in-depth-symbols/) на hacks.mozilla.org (2015)