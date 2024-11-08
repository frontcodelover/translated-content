---
title: "<em>: Элемент акцентирования"
slug: Web/HTML/Element/em
---

{{HTMLSidebar}}

**HTML `<em>` элемент** отмечает акцентируемый текст. Элемент `<em>` может быть вложенным, причём каждый уровень вложенности указывает на большую степень акцента.

| [Категории контента](/ru/docs/Web/HTML/Content_categories) | [Потоковый контент](/ru/docs/Web/HTML/Content_categories#Flow_content), [фразовый контент](/ru/docs/Web/HTML/Content_categories#Phrasing_content), явный контент. |
| ---------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Допустимый контент                                         | [Фразовый контент](/ru/docs/Web/HTML/Content_categories#Phrasing_content).                                                                                        |
| Пропуск тегов                                              | Нет, открывающий и закрывающий теги обязательны.                                                                                                                  |
| Допустимые родители                                        | Любой элемент, который принимает [фразовый контент](/ru/docs/Web/HTML/Content_categories#Phrasing_content).                                                       |
| Допустимые ARIA-роли                                       | Любые                                                                                                                                                             |
| DOM-интерфейс                                              | {{domxref ("HTMLElement")}} до Gecko 1.9.2 (Firefox 4) включительно Firefox реализует интерфейс {{domxref ("HTMLSpanElement")}} для этого элемента.               |

## Атрибуты

К этому элементу применимы [глобальные атрибуты](/ru/docs/Web/HTML/Общие_атрибуты).

## Примечания по использованию

Элемент `<em>` предназначен для слов, которые имеют подчёркнутый акцент по сравнению с окружающим текстом, который часто ограничивается словом или словами предложения и влияет на смысл самого предложения.

Обычно этот элемент отображается курсивом. Однако его не следует использовать просто для применения курсивного стиля; для этой цели используйте свойство CSS {{cssxref("font-style")}}. Используйте элемент {{HTMLElement("cite")}}, чтобы пометить название произведения (книги, пьесы, песни и т. д.). Используйте элемент {{HTMLElement("i")}}, чтобы пометить текст в альтернативном тоне или настроении, который охватывает многие распространённые ситуации курсива, такие как научные имена или слова на других языках. Используйте элемент {{HTMLElement("strong")}}, чтобы пометить текст, который имеет большее значение, чем окружающий текст.

### < i> против \<em>

Новые разработчики часто путаются, видя несколько элементов, которые дают аналогичные результаты. `<em>` и `<i>` являются общим примером, поскольку они оба выделяют текст курсивом. Какая разница? Что вы должны использовать?

По умолчанию визуальный результат тот же. Однако смысловое значение здесь другое. Элемент `<em>` представляет ударение на его содержании, в то время как элемент `<i>` представляет текст, который отличается от обычной прозы, например, иностранное слово, изречения вымышленного персонажа или когда текст ссылается на определение слова вместо представления его семантического значения. (Для названия произведения, например названия книги или фильма, следует использовать `<cite>`.)

Это означает, что правильное использование зависит от ситуации. Ни для чисто декоративных целей, это то, для чего предназначен CSS-стиль.

Примером для `<em>` может быть: -«Просто _сделай_ это!», или: «Мы _должны_ были что-то с этим сделать». Человек или программа, читающие текст, будут произносить слова, выделенные курсивом, с ударением, используя словесное ударение.

Примером для `<i>` может быть: _«Королева Мэри_ отплыла прошлой ночью». Здесь нет никакого дополнительного акцента или важности на слове "Королева Мэри". Просто указывается, что речь идёт не о королеве по имени Мария, а о корабле по имени _Королева Мария_. Другим примером для `<i>` может быть: «Слово _'the'_ это артикль».

## Пример

Элемент `<em>` часто используется для указания неявного или явного контраста.

```html
<p>
  В HTML 5, что ранее называлось контентом <em>уровня блока</em> теперь
  называется контентом <em>потока</em>.
</p>
```

### Результат

{{ EmbedLiveSample('Пример') }}

## Спецификации

{{Specifications}}

## Совместимость с браузерами

{{Compat}}

## Смотрите также

- {{HTMLElement("i")}}