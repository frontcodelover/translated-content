---
title: Список селекторов
slug: Web/CSS/Selector_list
l10n:
  sourceCommit: be7a098e6af7b820c06a2d5169a9221ee2065e82
---

{{CSSRef}}

**Список селекторов** CSS (`,`) выбирает все соответствующие ноды. Он состоит из набора селекторов разделённых запятыми.

## Описание

Когда селекторы используют одинаковые CSS-правила, они могут быть сгруппированы в разделённый запятыми список. Списки селекторов также могут передаваться в качестве параметра в некоторые функциональные CSS-псевдоклассы. Можно использовать пробельный символ перед и/или после запятой.

Следующие три записи эквивалентны:

```css
span {
  border: red 2px solid;
}
div {
  border: red 2px solid;
}
```

```css
span,
div {
  border: red 2px solid;
}
```

```css
:is(span, div) {
  border: red 2px solid;
}
```

## Синтаксис

```
element, element, element { свойства стиля }
```

## Примеры

Группировка селекторов в списки при применении одинаковых стилей к разным элементам позволяет одновременно как улучшить консистентность, так и уменьшить размер таблицы стилей.

### Группирование на одной строке

Группирование селекторов списком, разделённым запятыми, на одной строке.

```css-nolint
h1, h2, h3, h4, h5, h6 {
  font-family: helvetica;
}
```

### Многострочное группирование

Группирование селекторов списком, разделённым запятыми, на нескольких строках.

```css
#main,
.content,
h1 + p {
  font-size: 1.1em;
}
```

### Валидные и невалидные списки селекторов

Невалидный селектор ничему не соответствует. Когда список селекторов содержит хотя бы один невалидный селектор, весь блок стилей будет проигнорирован. Исключениями из этого правила являются псевдоклассы {{CSSxRef(":is", ":is()")}} и {{CSSxRef(":where", ":where()")}} принимающие [прощающий список селекторов](#прощающий_список_селекторов).

### Невалидный список селекторов

Недостатком использования списка селекторов является то, что один неподдерживаемый селектор в списке селекторов делает недействительным всё правило.

Рассмотрим два следующих набора CSS-правил:

```css
h1 {
  font-family: sans-serif;
}
h2:invalid-pseudo {
  font-family: sans-serif;
}
h3 {
  font-family: sans-serif;
}
```

```css
h1,
h2:invalid-pseudo,
h3 {
  font-family: sans-serif;
}
```

Они не эквивалентны. В первом наборе правил стили будут применены к элементам `h1` и `h3`, но правило`h2:invalid-pseudo` будет проигнорировано. Во втором наборе все правила будут проигнорированы, потому что один селектор в списке невалиден. Из-за этого ни один стиль не будет применён к элементам `h1` и `h3`, так как если любой селектор в списке селекторов невалиден, весь блок стилей будет проигнорирован.

### Прощающий список селекторов

Способом исправить проблему [невалидного списка селекторов](#невалидный_список_селекторов) является использование псевдоклассов {{CSSxRef(":is", ":is()")}} и {{CSSxRef(":where", ":where()")}}, которые принимают прощающий список селекторов. Каждый селектор в прощающем списке анализируется индивидуально. Поэтому любые невалидные селекторы в списке игнорируются и используются оставшиеся валидные.

Продолжая предыдущий пример, следующие два набора CSS-правил теперь эквивалентны:

```css
h1 {
  font-family: sans-serif;
}
h2:maybe-unsupported {
  font-family: sans-serif;
}
h3 {
  font-family: sans-serif;
}
```

```css
:is(h1, h2:maybe-unsupported, h3) {
  font-family: sans-serif;
}
```

Разница между `:is()` и `:where()` в том, что специфичность `:is()` равна его наиболее специфичному аргументу, тогда как селектор `:where()` и прощающий список селекторов в качестве его параметра не добавляют какой-либо специфичности.

### Список относительных селекторов

Таким списком является список [относительных селекторов](/ru/docs/Web/CSS/CSS_selectors/Selector_structure#относительный_селектор) разделённых запятыми и начинающихся с явного или предполагаемого комбинатора.

```css
h2:has(+ p, + ul.red) {
  font-style: italic;
}
```

В примере выше курсив будет применён к любому заголовку `h2` за которым сразу же следует `<p>` или `<ul class="red">`. Обратите внимание на то, что псевдоэлементы и селектор `:has()` не валидны внутри списка относительных селекторов [`:has()`](/ru/docs/Web/CSS/:has).

## Спецификации

{{Specifications}}

## Совместимость с браузерами

{{Compat}}

## Смотрите также

- Псевдоклассы [`:is()`](/ru/docs/Web/CSS/:is) и [`:where()`](/ru/docs/Web/CSS/:where) принимающие прощающий список селекторов.
- Псевдокласс [`:not()`](/ru/docs/Web/CSS/:not) принимающий список обычных селекторов.
- Псевдокласс [`:has()`](/ru/docs/Web/CSS/:has) принимающий список относительных селекторов.
- [CSS-селекторы](/ru/docs/Web/CSS/CSS_selectors)