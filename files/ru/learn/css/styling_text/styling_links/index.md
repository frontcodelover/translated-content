---
title: Стилизация ссылок
slug: Learn/CSS/Styling_text/Styling_links
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/CSS/Styling_text/Styling_lists", "Learn/CSS/Styling_text/Web_fonts", "Learn/CSS/Styling_text")}}

При стилизации ссылок, важно понимать как использовать псевдоклассы, чтобы стилизировать состояния ссылок эффективно, и как стилизировать ссылки для использования в общих разнообразных функциях интерфейса: таких как например навигационное меню и вкладки. Мы рассмотрим все эти темы в этой статье.

| Для изучения вам потребуется: | Основы компьютерной грамотности, базовые знания HTML (изучите [Введение в HTML](/ru/docs/Learn/HTML/Introduction_to_HTML)), основы CSS (изучите [Введение в CSS](/ru/docs/Learn/CSS/First_steps)), [базовые знания о текстах и шрифтах CSS](/ru/docs/Learn/CSS/Styling_text/Fundamentals). |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Вы узнаете:                   | Изучите как стилизуются ссылки и как использовать ссылки эффективно в общих задачах UI (пользовательских интерфейсах), например, в меню навигации.                                                                                                                                         |

## Давайте посмотрим на некоторые ссылки

Мы рассматривали как реализуются ссылки в вашем HTML в соответствии с лучшими практиками в [Создании гиперссылок](/ru/docs/Learn/HTML/%D0%92%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5_%D0%B2_HTML/%D0%A1%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5_%D0%B3%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BE%D0%BA). В этой статье мы будем опираться на эти знания, показывая вам лучшие практики по оформлению ссылок.

### Состояния ссылок

Первое, что нужно понять, это концепция состояний ссылок — разные состояния в которых могут существовать ссылки, которые могут быть стилизованы используя различные [псевдоклассы](/ru/docs/Learn/CSS/Building_blocks/Selectors#pseudo-classes):

- **Link (не посещённая)**: Состояние по умолчанию, в котором находится ссылка, когда она не находится в каком-либо другом состоянии. Она может быть специфически стилизована используя псевдокласс {{cssxref(":link")}}.
- **Visited**: Ссылка, когда она уже была посещена (существует в истории браузера), стилизуется используя псевдокласс {{cssxref(":visited")}}.
- **Hover**: Ссылка, когда на неё наведён курсор мыши, стилизуется используя псевдокласс {{cssxref(":hover")}}
- **Focus**: Ссылка, когда она была сфокусирована (например когда пользователь переместился на неё используя клавишу&#x20;

  <kbd>Tab</kbd>

  &#x20;или наподобие или программно сфокусирована используя {{domxref("HTMLElement.focus()")}}) — стилизуется используя псевдокласс {{cssxref(":focus")}}.

- **Active**: Ссылка, когда она активируется (например при клике по ней), стилизуется используя псевдокласс {{cssxref(":active")}}

### Стили по умолчанию

Следующий пример показывает, как будет вести себя ссылка по умолчанию (CSS просто увеличивает и центрирует текст чтоб больше выделить его).

```html
<p><a href="https://mozilla.org">A link to the Mozilla homepage</a></p>
```

```css
p {
  font-size: 2rem;
  text-align: center;
}
```

{{ EmbedLiveSample('Default_styles', '100%', 120) }}

Вы заметите несколько вещей при изучении стилей по умолчанию:

- Ссылки подчёркнуты.
- Не посещённые ссылки синие.
- Посещённые ссылки фиолетовые
- Наведение курсора мыши на ссылку меняют указатель мыши на иконку маленькой руки.
- Сфокусированные ссылки имеют контур вокруг себя — вы можете сфокусироваться на ссылках на этой странице с помощью клавиатуры, нажав клавишу табуляции (на Mac, вам может понадобиться включить опцию _Full Keyboard Access: All controls_ нажав&#x20;

  <kbd>Ctrl</kbd>

  &#x20;\+&#x20;

  <kbd>F7</kbd>

  , прежде чем это будет работать).

- Активные ссылки красные (попробуйте удерживать кнопку мыши на ссылке, когда вы кликните по ней).

Довольно интересно, что эти стили по умолчанию приблизительно такие же какими они были в первые дни браузеров в середине 1990-ых. Это потому, что пользователи знают и привыкли ожидать такого поведения — если бы ссылки были стилизованы по-разному, это бы путало много людей. Это не значит, что вы не должны стилизовать ссылки совсем, просто вы не должны уходить слишком далеко от ожидаемого поведения. По крайней мере вы должны:

- Использовать нижнее подчёркивание для ссылок, но не для других вещей. Если вы не хотите подчёркивать ссылки, то хотя бы выделите их каким-либо другим путём.
- Сделать так чтобы они как-нибудь реагировали на наведение/фокусировку на них и немного отличались после активации.

Стили по умолчанию могут быть выключены/изменены, используя следующие свойства CSS:

- {{cssxref("color")}} для цвета текста.
- {{cssxref("cursor")}} для стиля курсора мыши — вы не должны отключать эту опцию только если у вас нет на это веской причины.
- {{cssxref("outline")}} для контура текста (контур схож с границей, единственное отличие — это то, что границы занимают место в блоке, а контур — нет; он просто располагается поверх фона). Контур является полезным вспомогательным средством, так что подумайте хорошо, прежде чем отключать его; по крайней мере вы должны удвоить стили, заданные для состояния hover, а также состояния фокусировки.

> [!NOTE]
> Вы не ограничены только перечисленными выше свойствами чтобы стилизовать ссылки — вы можете использовать любые свойства, которые вам нравятся. Просто постарайтесь не сходить с ума слишком сильно!

### Стилизация некоторых ссылок

Мы уже рассмотрели состояния по умолчанию в некоторых деталях, давайте взглянем на типичный набор стилей ссылок.

Чтобы начать, мы выпишем наши пустые наборы правил:

```css
a {
}

a:link {
}

a:visited {
}

a:focus {
}

a:hover {
}

a:active {
}
```

Этот порядок важен так как стили ссылок опираются друг на друга, например стили в первом правиле будут применяться ко всем последующим правилам и когда ссылка будет активирована, она также будет находиться под "наведением" (hover). Если вы введёте их в неправильном порядке, стили не будут работать правильно. Чтобы запомнить этот порядок вы можете попробовать использовать мнемонику типа **L**o**V**e **F**ears **HA**te.

А теперь давайте добавим ещё немного информации чтобы правильно оформить этот стиль:

```css
body {
  width: 300px;
  margin: 0 auto;
  font-size: 1.2rem;
  font-family: sans-serif;
}

p {
  line-height: 1.4;
}

a {
  outline: none;
  text-decoration: none;
  padding: 2px 1px 0;
}

a:link {
  color: #265301;
}

a:visited {
  color: #437a16;
}

a:focus {
  border-bottom: 1px solid;
  background: #bae498;
}

a:hover {
  border-bottom: 1px solid;
  background: #cdfeaa;
}

a:active {
  background: #265301;
  color: #cdfeaa;
}
```

Также мы дадим некий пример HTML к которому применяется CSS:

```html
<p>
  There are several browsers available, such as
  <a href="https://www.mozilla.org/en-US/firefox/">Mozilla Firefox</a>,
  <a href="https://www.google.com/chrome/index.html">Google Chrome</a>, and
  <a href="https://www.microsoft.com/en-us/windows/microsoft-edge"
    >Microsoft Edge</a
  >.
</p>
```

Объединение этих двух даёт нам такой результат:

{{ EmbedLiveSample('Styling_some_links', '100%', 150) }}

Итак, что мы сделали тут? Это определённо выглядит иначе чем стилизация по умолчанию, но все ещё даёт достаточно знакомый опыт для пользователей, чтобы знать, что происходит:

- Первые два правила не так интересны в этом обсуждении.
- Третье правило использует селектор `a` чтобы избавиться от подчёркивания текста и контура фокуса по умолчанию (которые всё равно варьируют в зависимости от браузера), а также добавляет малое количество padding к каждой ссылке — все это станет ясно позже.
- Далее, мы используем селекторы `a:link` и `a:visited` чтобы настроить пару цветовых вариаций не посещённых и посещённых ссылок, так чтоб они отличались.
- Следующие два правила используют `a:focus` и `a:hover` настраивают сфокусированные и наведённые (hovered) ссылки таким образом чтобы они имели разные фоновые цвета, плюс нижнее подчёркивание чтобы ссылка выделялась ещё больше. Два пункта на которые надо обратить внимание:

  - Нижнее подчёркивание создано используя {{cssxref("border-bottom")}}, а не {{cssxref("text-decoration")}} — некоторые люди предпочитают это потому что первый имеет лучшие варианты стилизации, чем второй, и отрисован немного ниже, так что не срезает нижние элементы слов будучи подчёркнутыми (например хвосты у букв как "р" и "у").
  - Значение {{cssxref("border-bottom")}} установлено на `1px solid`, без определённого цвета. Это позволяет границам принимать тот же цвет что и элементы текста, что полезно в случае как этом, где текст имеет разные цвета в каждом случае.

- Наконец, `a:active` используется чтобы дать ссылкам инвертированную цветовую схему в то время когда они активированы, чтобы было ясно что происходит что то важное!

### Активное изучение: Стилизуйте ссылки самостоятельно

В этой секции активного изучения, мы бы хотели, чтобы взяли наш набор пустых правил и добавили ваши собственные объявления так чтобы ссылки выглядели действительно круто. Используйте своё воображение, не сковывайтесь. Мы уверены, что вы можете придумать что-то более крутое и все ещё так же функциональное, как и наш пример выше.

Если вы допустите ошибку, вы всегда можете сделать сброс используя кнопку _Reset_. Если вы действительно застряли нажмите кнопку _Show solution_ чтобы вставить пример, который мы показали выше.

```html hidden
<div
  class="body-wrapper"
  style="font-family: 'Open Sans Light',Helvetica,Arial,sans-serif;">
  <h2>HTML Input</h2>
  <textarea
    id="code"
    class="html-input"
    style="width: 90%;height: 10em;padding: 10px;border: 1px solid #0095dd;">
<p>There are several browsers available, such as <a href="https://www.mozilla.org/en-US/firefox/">Mozilla
 Firefox</a>, <a href="https://www.google.com/chrome/index.html">Google Chrome</a>, and
<a href="https://www.microsoft.com/en-us/windows/microsoft-edge">Microsoft Edge</a>.</p></textarea
  >

  <h2>CSS Input</h2>
  <textarea
    id="code"
    class="css-input"
    style="width: 90%;height: 10em;padding: 10px;border: 1px solid #0095dd;">
a {

}

a:link {

}

a:visited {

}

a:focus {

}

a:hover {

}

a:active {

}</textarea
  >

  <h2>Output</h2>
  <div
    class="output"
    style="width: 90%;height: 10em;padding: 10px;border: 1px solid #0095dd;"></div>
  <div class="controls">
    <input
      id="reset"
      type="button"
      value="Reset"
      style="margin: 10px 10px 0 0;" />
    <input
      id="solution"
      type="button"
      value="Show solution"
      style="margin: 10px 0 0 10px;" />
  </div>
</div>
```

```js hidden
var htmlInput = document.querySelector(".html-input");
var cssInput = document.querySelector(".css-input");
var reset = document.getElementById("reset");
var htmlCode = htmlInput.value;
var cssCode = cssInput.value;
var output = document.querySelector(".output");
var solution = document.getElementById("solution");

var styleElem = document.createElement("style");
var headElem = document.querySelector("head");
headElem.appendChild(styleElem);

function drawOutput() {
  output.innerHTML = htmlInput.value;
  styleElem.textContent = cssInput.value;
}

reset.addEventListener("click", function () {
  htmlInput.value = htmlCode;
  cssInput.value = cssCode;
  drawOutput();
});

solution.addEventListener("click", function () {
  htmlInput.value = htmlCode;
  cssInput.value =
    "p {\n  font-size: 1.2rem;\n  font-family: sans-serif;\n  line-height: 1.4;\n}\n\na {\n  outline: none;\n  text-decoration: none;\n  padding: 2px 1px 0;\n}\n\na:link {\n  color: #265301;\n}\n\na:visited {\n  color: #437A16;\n}\n\na:focus {\n  border-bottom: 1px solid;\n  background: #BAE498;\n}\n\na:hover {\n  border-bottom: 1px solid;\n  background: #CDFEAA;\n}\n\na:active {\n  background: #265301;\n  color: #CDFEAA;\n}";
  drawOutput();
});

htmlInput.addEventListener("input", drawOutput);
cssInput.addEventListener("input", drawOutput);
window.addEventListener("load", drawOutput);
```

{{ EmbedLiveSample('Playable_code', 700, 800) }}

## Добавление иконок в ссылки

Обычной практикой является добавление иконок в ссылки, чтобы предоставить больше индикатора того, на какой контент указывает ссылка. Давайте рассмотрим очень простой пример, который добавляет иконку к внешним ссылкам (ссылки, которые ведут на другие сайты). Такая ссылка обычно выглядит как маленькая стрела торчащая из коробочки — например, мы будем использовать [этот отличный образец с сайта icons8.com](https://icons8.com/web-app/741/external-link).

Давайте взглянем на HTML и CSS которые дадут нам эффект, который мы хотим. Во-первых, немного простого HTML который будет стилизован:

```html
<p>
  For more information on the weather, visit our
  <a href="weather.html">weather page</a>, look at
  <a href="https://en.wikipedia.org/wiki/Weather">weather on Wikipedia</a>, or
  check out
  <a href="http://www.extremescience.com/weather.htm"
    >weather on Extreme Science</a
  >.
</p>
```

Далее, CSS:

```css
body {
  width: 300px;
  margin: 0 auto;
  font-family: sans-serif;
}

p {
  line-height: 1.4;
}

a {
  outline: none;
  text-decoration: none;
  padding: 2px 1px 0;
}

a:link {
  color: blue;
}

a:visited {
  color: purple;
}

a:focus,
a:hover {
  border-bottom: 1px solid;
}

a:active {
  color: red;
}

a[href*="http"] {
  background: url("external-link-52.png") no-repeat 100% 0;
  background-size: 16px 16px;
  padding-right: 19px;
}
```

{{ EmbedLiveSample('Including_icons_on_links', '100%', 150) }}

Итак, что же тут происходит? Мы пропустим большую часть CSS так как это та же информация, которую вы рассматривали ранее. Однако, последнее правило интересное — тут мы вставляем пользовательское фоновое изображение во внешнюю ссылку схожим способом как мы делали [пользовательские маркеры для пунктов списка](/ru/docs/Learn/CSS/Styling_text/Styling_lists#using_a_custom_bullet_image) в последней статье — в этот раз, однако, мы используем короткую запись {{cssxref("background")}} вместо индивидуальных свойств. Мы задаём путь к изображению, которое хотим вставить, устанавливаем `no-repeat` чтобы мы получили только одну копию вставленного и затем устанавливаем позицию на 100% до правого края изображения и 0 пикселей от верхнего края.

Также мы используем {{cssxref("background-size")}} для того чтобы указать размер в котором бы хотим чтобы было показано фоновое изображение — полезно иметь иконку большего размера и далее менять его размер так, как нужно для адаптивного (отзывчивого) веб-дизайна. Однако это работает только в IE9 и следующих версиях так что, если вам нужна поддержка тех старых браузеров вам просто придётся менять размер изображения и вставлять его как есть.

Наконец, мы задаём некоторый {{cssxref("padding-right")}} для ссылки чтобы добавить пространство в котором появляется фоновое изображение, таким образом, чтобы мы не накладывали его на текст.

И последнее слово — как мы выбрали только внешние ссылки? Ну, если вы пишете свои [HTML ссылки](/ru/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks) правильно, то вы должны были использовать только абсолютные URL для внешних ссылок — гораздо эффективнее использовать относительные ссылки для связи с другими частями вашего сайта. Текст "http" таким образом должен появляться только во внешних ссылках и можем выбрать его при помощи [селектора атрибутов](/ru/docs/Learn/CSS/Building_blocks/Selectors#attribute_selectors): `a[href*="http"]` выбирает элементы {{htmlelement("a")}}, но только если они имеют атрибут [`href`](/ru/docs/Web/HTML/Element/a#href) со значением содержащим "http" где-то внутри него.

Ну вот и все — попробуйте посетить секцию активного изучения выше и испытайте этот новый метод!

> [!NOTE]
> Не переживайте если вы ещё не знакомы с [фоном](/ru/docs/Learn/CSS/Building_blocks) и [адаптивным (отзывчивым) веб-дизайном](/ru/docs/Web/Progressive_web_apps/Responsive/responsive_design_building_blocks); это объяснено в других местах

## Стилизация ссылок в виде кнопок

Инструменты, которые вы исследовали в этой статье также могут быть использованы другим способом. Например, такие состояния как hover могут быть использованы для стилизации множества различных элементов, не только ссылок — вы можете захотеть стилизовать состояние hover параграфов, элементов списка или других вещей.

Дополнительно, ссылки очень часто стилизуют так, чтоб они выглядели и вели себя как кнопки при определённых обстоятельствах — навигационное меню веб-сайтов обычно размечено как список, содержащий ссылки, который легко может быть стилизован так чтоб выглядел как набор кнопок управления или вкладок которые обеспечивают пользователя доступом к другим частям сайта. Давайте изучим как.

Для начала HTML:

```html
<ul>
  <li><a href="#">Home</a></li>
  <li><a href="#">Pizza</a></li>
  <li><a href="#">Music</a></li>
  <li><a href="#">Wombats</a></li>
  <li><a href="#">Finland</a></li>
</ul>
```

А теперь наш CSS:

```css
body,
html {
  margin: 0;
  font-family: sans-serif;
}

ul {
  padding: 0;
  width: 100%;
}

li {
  display: inline;
}

a {
  outline: none;
  text-decoration: none;
  display: inline-block;
  width: 19.5%;
  margin-right: 0.625%;
  text-align: center;
  line-height: 3;
  color: black;
}

li:last-child a {
  margin-right: 0;
}

a:link,
a:visited,
a:focus {
  background: yellow;
}

a:hover {
  background: orange;
}

a:active {
  background: red;
  color: white;
}
```

Что даёт нам следующий результат:

{{ EmbedLiveSample('Styling_links_as_buttons', '100%', 100) }}

Давайте объясним, что тут происходит, фокусируясь на самых интересных частях:

- Наше второе правило удаляет заданный по умолчанию {{cssxref("padding")}} у элемента {{htmlelement("ul")}} и устанавливает его ширину так, чтобы охватить 100% внешнего контейнера (в этом случае {{htmlelement("body")}}).
- Элементы {{htmlelement("li")}} по умолчанию в норме являются блочными (см. [типы блоков CSS](/ru/docs/Learn/CSS/Building_blocks/The_box_model#types_of_css_boxes) чтобы вспомнить), что значит что они будут располагаться на своих собственных строках. В этом случае мы создаём горизонтальный список ссылок, поэтому в третьем правиле задаём свойству {{cssxref("display")}} значение inline, что приводит к тому, что элементы списка располагаются в одной строке друг с другом — теперь они ведут себя как строчные элементы.
- четвёртое правило — которое стилизует элемент {{htmlelement("a")}} — самое сложное; давайте пройдёмся по нему шаг за шагом:

  - как в предыдущем примере, мы начинаем отключать настройки по умолчанию для {{cssxref("text-decoration")}} и {{cssxref("outline")}} — мы не хотим, чтоб они портили нам вид.
  - Далее мы устанавливаем {{cssxref("display")}} на `inline-block` — элементы {{htmlelement("a")}} являются строчными по умолчанию и, поскольку мы не хотим чтобы они вываливались на свои собственные строки как если бы это получалось со значением `block`, мы хотим иметь возможность менять их размер. `inline-block` позволяет нам делать это.
  - Теперь только изменение размера! Мы хотим заполнить всю ширину элемента {{htmlelement("ul")}}, оставить немного margin между каждой кнопкой (не без зазора с правого края) и мы имеем 5 кнопок, которые надо разместить и которые должны иметь одинаковый размер. Для того чтобы это сделать мы задаём {{cssxref("width")}} на 19.5%, а {{cssxref("margin-right")}} на 0.625%. Вы заметите что вся эта эта ширина составляет 100.625%, что может сделать так что последняя кнопка перекроет `<ul>` и выпадет вниз на следующую строку. Тем не менее, мы возвращаемся к 100%, используя следующее правило, которое выбирает только последний `<a>` в списке и удаляет его margin. Сделано!
  - Последние три объявления довольно просты и в основном просто для косметических целей. Мы центрируем текст внутри каждой ссылки, задаём {{cssxref("line-height")}} на 3 чтобы кнопки имели некую высоту (что также имеет преимущество в центрировании текста по вертикали) и задаём для текста чёрный цвет.

> [!NOTE]
> Вы могли заметить что элементы списка в HTML все находятся на одной строке друг с другом — так сделано потому, что это сделано потому, что пробелы/разрывы строк между элементами встроенного блока создают пробелы на странице, точно также как пробелы между словами и такие пробелы могли бы нарушить расположение нашего горизонтального меню навигации. Вы можете найти больше информации об этой проблеме (и решения) на [Fighting the space between inline block elements](https://css-tricks.com/fighting-the-space-between-inline-block-elements/).

## Заключение

Мы надеемся эта статья снабдила вас всем что вам надо знать о ссылках — на данный момент! Последняя статья в нашем модуле стилизации текста детализирует как использовать пользовательские шрифты на вашем веб-сайте или как они больше известны веб-шрифты.

{{PreviousMenuNext("Learn/CSS/Styling_text/Styling_lists", "Learn/CSS/Styling_text/Web_fonts", "Learn/CSS/Styling_text")}}