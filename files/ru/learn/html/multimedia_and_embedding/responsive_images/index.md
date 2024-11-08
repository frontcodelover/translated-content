---
title: Адаптивные изображения
slug: Learn/HTML/Multimedia_and_embedding/Responsive_images
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/HTML/Multimedia_and_embedding/Adding_vector_graphics_to_the_Web", "Learn/HTML/Multimedia_and_embedding/Mozilla_splash_page", "Learn/HTML/Multimedia_and_embedding")}}

В данной статье мы изучим концепцию гибких (responsive) изображений — таких, которые отображаются хорошо на устройствах с сильно отличающимися размерами экрана, разрешением, и другими характеристиками — и рассмотрим инструменты, которые имеются в HTML для их реализации. Responsive images - только одна часть (и хорошее начало) гибкого веб-дизайна, темы, которая будет рассмотрена подробнее в будущем модуле на тему [CSS](/ru/docs/Learn/CSS).

| Требования: | Предполагается, что вы уже знакомы с [основами HTML](/ru/docs/Learn/HTML/Introduction_to_HTML) и умеете [добавлять статичные изображения на веб-страницу](/ru/docs/Learn/HTML/Multimedia_and_embedding/Images_in_HTML). |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Цель:       | Узнать, как использовать такие элементы, как [`srcset`](/ru/docs/Web/HTML/Element/img#srcset) и {{htmlelement("picture")}} чтобы обеспечить работу гибких изображения на веб-сайтах.                                    |

## Почему адаптивные изображения?

Какую проблему мы пытаемся решить адаптивными изображениями? Давайте рассмотрим типичный сценарий. Обычный веб-сайт может содержать изображение в заголовке, для улучшения визуального восприятия пользователем, а также несколько изображений в контенте под ним. Вы, вероятно, захотите, чтобы изображение в заголовке занимало всю ширину окна, а изображения в контенте размещались где-то внутри колонки с контентом. Давайте посмотрим на следующий простой пример:

![Our example site as viewed on a wide screen - here the first image works ok, as it is big enough to see the detail in the center.](picture-element-wide.png)

Такая вёрстка хорошо выглядит на широкоформатных экранах ноутбуков и настольных ПК, (вы можете посмотреть [посмотреть демо-пример](http://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/not-responsive.html) и найти [исходный код](https://github.com/mdn/learning-area/blob/master/html/multimedia-and-embedding/responsive-images/not-responsive.html) на Github.) Мы не будем подробно рассматривать CSS, скажем только следующее:

- Содержимому тега `main` задана максимальная ширина 1200 пикселей. Если ширина окна браузера больше этого значения, то содержимое сайта остаётся на 1200 пикселей и центрирует себя в доступном пространстве. Если ширина окна браузера меньше, содержимое устанавливается в 100% от ширины экрана.
- Изображение в шапке всегда будет оставаться в центре тега header вне зависимости от ширины браузера. Если сайт будет просматриваться на узких экранах, то важные детали в центре изображения (люди) всё равно будут видны. Все, что выходит за пределы ширины экрана будет скрыто. Высота шапки 200 пикселей.
- Изображения в содержимом заданы так, что если ширина body становится меньше чем ширина изображения, то изображения начинают сжиматься и остаются всегда внутри body и не выступают за его пределы.

Всё хорошо, однако проблемы начинаются, когда вы просматриваете сайт на устройстве с небольшим экраном – шапка внизу выглядит нормально, но теперь она занимает значительную высоту экрана; первое изображение в контенте напротив, выглядит ужасно – при таком размере едва можно рассмотреть людей!

![Our example site as viewed on a narrow screen; the first image has shrunk to the point where it is hard to make out the detail on it.](non-responsive-narrow.png)

Было бы намного лучше показывать обрезанную версию изображения, на котором видны важные детали снимка, когда сайт отображается на узком экране, и, возможно, что-то среднее между обрезанным и оригинальным изображениями для экранов средней ширины, таких как планшеты – это известно как **art direction problem**.

Кроме того, нет нужды встраивать такие большие изображения на страницу, если она просматривается на маленьком экране мобильного устройства; это называется **resolution switching problem** — растровое изображение представляет собой точно-заданное количество пикселей по ширине и высоте; как мы успели заметить, когда рассматривали [векторную графику](/ru/docs/Learn/HTML/Multimedia_and_embedding/Adding_vector_graphics_to_the_Web), растровое изображение становится зернистым и выглядит ужасно, если оно отображается в размере большем, чем оригинальный (тогда как векторное изображение нет). В то же время, если изображение отображается в гораздо меньшем размере, чем оригинальный, это приведёт к напрасной трате трафика — пользователи мобильных устройств будут грузить большое изображение для компьютера, вместо маленького для их устройства. Идеально было бы иметь несколько файлов в разных разрешениях, и отображать нужный размер в зависимости от устройства, обращающегося к веб-сайту.

Сложность в том, что для некоторых устройств с большим разрешением экрана нужны изображения большего чем ожидается размера, чтобы чётче отображалось. По сути это всё одна задача в разных условиях.

Можно предположить, что векторные изображения могли бы решить эти проблемы. В какой-то степени это так. У них небольшой вес и размер, поэтому их можно использовать почти в любом случае. Они хороши для простой графики, узоров, элементов интерфейса и т. д. Сложнее создать векторное изображение с большим количеством деталей, как, например, на фото. Растровые изображения (JPEG) для нашего примера подходят больше.

Такого рода проблемы не было в начале существования веба, в первой половине 90-х годов – тогда единственными устройствами для просмотра веб-страниц были настольные компьютеры и ноутбуки, так что создатели браузеров и авторы спецификаций даже не задумывались о создании решения. _Технологии отзывчивых изображений_ были реализованы недавно для решения проблем, указанных выше. Они позволяют вам предоставить браузеру несколько изображений, каждое из которых отображает одно и то же, но содержит разное количество пикселей (_resolution switching_), или разные изображения с отдельными областями основного изображения (_art direction_).

> [!NOTE]
> Новые возможности обсуждаются в статье — [`srcset`](/ru/docs/Web/HTML/Element/img#srcset)/[`sizes`](/ru/docs/Web/HTML/Element/img#sizes)/{{htmlelement("picture")}} — все они поддерживаются последними версиями современных настольных и мобильных браузеров (включая Microsoft Edge, но не Internet Explorer).

## Как сделать изображения отзывчивыми?

В этом разделе рассмотрим две вышеописанные проблемы и покажем, как их решить с использованием инструментов HTML {{htmlelement("img")}}. Как показано на примере выше - изображение в заголовке используется только как украшение сайта и установлено как фоновое с помощью CSS. [CSS больше подходит для адаптивного дизайна](http://blog.cloudfour.com/responsive-images-101-part-8-css-images/) чем HTML, об этом поговорим в следующем модуле о CSS.

### Разные разрешения: Разные размеры

Итак, какую проблему решают разные разрешения? В зависимости от устройства нужно отобразить одно и то же изображение, но разных размеров. Посмотрите на вторую картинку в примере. Стандартный элемент {{htmlelement("img")}} обычно позволяет указать только один путь к файлу:

```html
<img src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy" />
```

Однако есть два новых атрибута — [`srcset`](/ru/docs/Web/HTML/Element/img#srcset) и [`sizes`](/ru/docs/Web/HTML/Element/img#sizes) — позволяющих добавить дополнительные изображения с пометками, чтобы браузер выбрал подходящее. Пример на Github: [responsive.html](http://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/responsive.html) (также смотри [источник кода](https://github.com/mdn/learning-area/blob/master/html/multimedia-and-embedding/responsive-images/responsive.html)).

```html
<img
  srcset="
    elva-fairy-320w.jpg 320w,
    elva-fairy-480w.jpg 480w,
    elva-fairy-800w.jpg 800w
  "
  sizes="(max-width: 320px) 280px,
            (max-width: 480px) 440px,
            800px"
  src="elva-fairy-800w.jpg"
  alt="Elva dressed as a fairy" />
```

Атрибуты `srcset` и `sizes` кажутся сложными, но они не так плохи, если вы отформатируете их как в примере выше: каждая часть значения атрибута с новой строки. Значение состоит из списка элементов через запятую, каждый из которых включает три части. Давайте рассмотрим эти значения:

**`srcset`** включает названия изображений, среди которых браузер выберет нужное и их размеры. Перед каждой запятой части значения в таком порядке:

1. Название изображения (`elva-fairy-480w.jpg`.)
2. Пробел.
3. **Актуальная ширина картинки** **в пикселах** (`480w`) — заметьте, что здесь используется `w` вместо `px`, как вы могли ожидать. Эта настоящая ширина изображения, которая может быть просмотрена в свойствах картинки на вашем компьютере (например, на Mac нужно открыть картинку в Finder и нажать&#x20;

   <kbd>Cmd</kbd>

   &#x20;\+&#x20;

   <kbd>I</kbd>

   &#x20;, чтобы вывести информацию на экран).

**`sizes`** определяет перечень медиавыражений (например, ширину экрана) и указывает предпочтительную ширину изображения, когда определённое медиавыражение истинно — это то, о чём мы говорили выше. В нашем случае, перед каждой запятой мы пишем:

1. **Медиа-условие** (`(max-width:480px)`) — вы можете больше узнать об этом в [CSS topic](/ru/docs/Learn/CSS), но сейчас давайте скажем, что медиа-условие описывает возможное состояние экрана. В этом случае, мы говорим "когда viewport width меньше или равен 480 пикселям".
2. Пробел.
3. **Ширину слота** (в оригинале "width of the slot"), занимаемую изображением, когда медиа-условие истинно. (`440px`)

> [!NOTE]
> Для ширины слота, вы можете указать абсолютные значения (`px`, `em`) или значение относительно окна просмотра (`vw`), но НЕ проценты. Вы могли заметить, что у последнего слота нет медиа-условия — это значение по умолчанию, которое станет актуальным, если ни одно из предыдущих медиа-условий не будет истинно. Браузер игнорирует все последующие проверки после первого совпадения, так что будьте внимательнее к порядку их объявления.

Итак, с такими атрибутами, браузер сделает следующее:

1. Посмотрит на ширину экрана устройства.
2. Попытается определить подходящее медиа-условие из списка в атрибуте `sizes`.
3. Посмотрит на размер слота к этому медиавыражению.
4. Загрузит изображение из списка из `srcset`, которое имеет тот же размер, что и выбранный слот, или, если такого нет, то первое изображение, которое больше размера выбранного слота.

И это всё! На текущий момент, если поддерживающий браузер с viewport width 480px загрузит страницу, медиа-условие `(max-width: 480px)` будет истинно, следовательно, будет выбран слот `440px`, тогда будет загружено изображение `elva-fairy-480w.jpg`, так как свойство ширины (`480w`) наиболее близко значение `440px`. Условно, изображение 800px занимает на диске 128KB, в то время как версия в 480px только 63KB — экономия в 65KB. Теперь представьте, что у вас страница, на которой много изображений. Используя это технику, вы обеспечите мобильным пользователям большую пропускную способность.

Старые браузеры, не поддерживающие эти возможности, просто проигнорируют их и возьмут изображение по адресу из атрибута [`src`](/ru/docs/Web/HTML/Element/img#src).

> [!NOTE]
> В описании элемента {{htmlelement("head")}} вы найдёте строку `<meta name="viewport" content="width=device-width">`: это заставляет мобильные браузеры адаптировать их реальный viewport width для загрузки web-страниц (некоторые мобильные браузеры нечестны насчёт своего viewport width, вместо этого они загружают страницу в большем viewport width, а затем ужимают её, что не очень хорошо сказывается на наших отзывчивых изображениях или дизайне. Мы расскажем вам об этом больше в будущем модуле.)

### Полезные инструменты разработчика

Есть несколько полезных браузерных [инструментов разработчика](/ru/docs/Learn/Common_questions/What_are_browser_developer_tools), чтобы помочь с определением необходимой ширины слотов и т. д., которые вам нужно использовать. Когда я работал над ними, я сначала загружал фиксированную версию моего примера (`not-responsive.html`), затем открывал [Responsive Design View](/ru/docs/Tools/Responsive_Design_Mode) (_Tools > Web Developer > Responsive Design View_), который позволяет взглянуть на layout вашей веб-страницы как если бы они были просмотрены через устройства с различными размерами экрана.

Я устанавливал viewport width на 320px, затем на 480px; для каждой я обращался к [DOM Inspector,](/ru/docs/Tools/Page_Inspector) кликал по элементу {{htmlelement("img")}} в котором мы заинтересованы, далее смотрел размер во вкладке Box Model с правой стороны дисплея. Это должно дать вам необходимую ширину изображения

![A screenshot of the firefox devtools with an image element highlighted in the dom, showing its dimensions as 440 by 293 pixels.](box-model-devtools.png)

А дальше вы можете проверить работает ли `srcset` если установить значение viewport width таким каким вы хотите (например, установить узкую ширину), открыв Network Inspector (_Tools > Web Developer > Network_) и затем перезагрузить страницу. Это должно дать вам перечень ресурсов которые были загружены чтобы составить (собрать) web-страницу, и тут вы можете проверить какой файл изображения был выбран для загрузки.

![a screenshot of the network inspector in firefox devtools, showing that the HTML for the page has been downloaded, along with three images, which include the two 800 wide versions of the responsive images](network-devtools.png)

### Переключения разрешений: Одинаковый размер, разные разрешения

Если вы поддерживаете несколько разрешений экрана, но все видят ваше изображение в одном и том же размере на экране, вы можете позволить браузеру выбирать изображение с подходящим разрешением используя `srcset` с x-дескриптором и без `sizes` — более простой синтаксис! Найти пример как это выглядит можно здесь [srcset-resolutions.html](http://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/srcset-resolutions.html) (смотрите также [the source code](https://github.com/mdn/learning-area/blob/master/html/multimedia-and-embedding/responsive-images/srcset-resolutions.html)):

```html
<img
  srcset="elva-fairy-320w.jpg, elva-fairy-480w.jpg 1.5x, elva-fairy-640w.jpg 2x"
  src="elva-fairy-640w.jpg"
  alt="Elva dressed as a fairy" />
```

![A picture of a little girl dressed up as a fairy, with an old camera film effect applied to the image](resolution-example.png)В данном примере, к изображению применяется CSS таким образом, что оно имеет ширину в 320 пикселей на экране (также называемое CSS-пикселями):

```css
img {
  width: 320px;
}
```

В этом случае, нет необходимости в `sizes` — браузер просто определяет в каком разрешении отображает дисплей и выводит наиболее подходящее изображение в соответствии с `srcset`. Таким образом, если устройство, подключаемое к странице, имеет дисплей стандартного/низкого разрешения, когда один пиксель устройства представляет (соответствует) каждый CSS-пиксель, то будет загружено изображение `elva-fairy-320w.jpg` (применён x1, то есть вам не надо включать его). Если устройство имеет высокое разрешение, в два пикселя устройства на каждый CSS-пиксель или более, то будет загружено изображение `elva-fairy-640w.jpg`. 640px изображение имеет размер 93KB, тогда так 320px изображение - всего 39KB.

### Художественное оформление

Подводя итоги, **проблема художественного оформления** заключается в желании изменить отображаемое изображение чтобы оно соответствовало разным размерам отображения изображения. Например, если на веб-сайте отображается большой пейзажный снимок с человеком посередине при просмотре в браузере на настольном компьютере, то при просмотре веб-сайта в мобильном браузере он уменьшается; он будет выглядеть плохо так как человек будет очень маленьким, и его будет тяжело разглядеть. Вероятно будет лучше показать меньшую портретную картинку в мобильной версии на которой человек отображается в увеличении (в приближении). Элемент {{htmlelement("picture")}} позволяет нам применять именно такое решение.

Возвращаясь к нашему оригинальному примеру [not-responsive.html](http://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/not-responsive.html), мы имеем изображение которое очень нуждается в художественном оформлении:

```html
<img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva" />
```

Давайте исправим это при помощи элемента {{htmlelement("picture")}}! Так же как [`<video>` и `<audio>`](/ru/docs/Learn/HTML/Multimedia_and_embedding/Video_and_audio_content), элемент `<picture>` это обёртка содержащая некоторое количество элементов {{htmlelement("source")}} которые предоставляют браузеру выбор нескольких разных источников, в сопровождении крайне важного элемента {{htmlelement("img")}}. Код [responsive.html](http://mdn.github.io/learning-area/html/multimedia-and-embedding/responsive-images/responsive.html) выглядит так:

```html
<picture>
  <source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg" />
  <source media="(min-width: 800px)" srcset="elva-800w.jpg" />
  <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva" />
</picture>
```

- Элемент `<source>` принимает атрибут `media`, который содержит медиа-условие; при помощи этих условий определяется, какое изображение будет выведено. В данном случае, если ширина viewport'a составит 799px или меньше, будет выведено изображение первого элемента `<source>`. Если ширина составит 800px и более — второго.
- Атрибут `srcset` содержит путь изображения, которое будет выведено. Обратите внимание, что, как и в примере с `<img>` выше, `<source>` может принимать атрибуты `srcset` и `sizes` с несколько предопределёнными изображениями. Так вы можете не только поместить группу изображений внутри элемента `<picture>`, но и задать группу предписаний для каждого из них. В реальности вы вряд ли захотите заниматься этим очень часто.
- Вы всегда должны использовать элемент `<img>`, с `src` и `alt`, прямо перед `</picture>`, иначе изображения не появятся. Это нужно на тот случай, когда ни одно из медиа-условий не удовлетворено (например, если бы вы убрали второй элемент `<source>)` или браузер не поддерживает элемент `<picture>`.

Этот код позволяет нам выводить отзывчивое изображение и на широких, и на узких экранах, как показано ниже:

![Our example site as viewed on a wide screen - here the first image works ok, as it is big enough to see the detail in the center.](picture-element-wide.png)![Our example site as viewed on a narrow screen with the picture element used to switch the first image to a portrait close up of the detail, making it a lot more useful on a narrow screen](/ru/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images/picture-element-narrow.png)

> [!NOTE]
> Вам следует использовать атрибут `media` только при художественном оформлении; когда вы используете `media`, не применяйте медиа-условия с атрибутом `sizes`.

### Почему это нельзя сделать посредством CSS и JavaScript?

Когда браузер начинает загружать страницу, он начинает загрузку изображений до того, как главный парсер начал загружать и интерпретировать CSS и JavaScript. В среднем, эта техника уменьшает время загрузки страницы на 20%. Но она не так полезна в случае с адаптивными изображениями, поэтому и необходимы такие решения, как `srcset`. Например, вы не могли бы загрузить элемент `<img>`, потом определить ширину вьюпорта при помощи JavaScript и динамически изменить источник изображения. Изначальное изображение было бы уже загружено к тому времени, как вы загрузили его меньшую версию, что плохо.

### Смело используйте современные форматы изображений

Есть несколько новых форматов изображения (таких, как WebP и JPEG-2000), которым удаётся сохранять высокое качество при малом размере файла. Тем не менее, браузеры поддерживают их не полностью.

`<picture>` позволяет нам использовать их в старых браузерах. Вы можете прописать MIME-тип внутри атрибута `type`, браузер сразу определит файлы такого типа как неподдерживаемые:

```html
<picture>
  <source type="image/svg+xml" srcset="pyramid.svg" />
  <source type="image/webp" srcset="pyramid.webp" />
  <img
    src="pyramid.png"
    alt="regular pyramid built from four equilateral triangles" />
</picture>
```

- Не используйте атрибут `media`, если вам не нужно художественное оформление.
- В элементе `<source>` можно указывать путь к изображениям только того типа, который указан в `type`.
- Как и в предыдущих примерах, при необходимости вы можете использовать `srcset` и `sizes`.

## Активное обучение: реализация собственных адаптивных изображений

Самостоятельно создайте отзывчивое, художественно оформленное изображение для широких и узких экранов, используя `<picture>` и `srcset`.

1. Напишите простую HTML-разметку.
2. Найдите широкоформатное пейзажное фото с какой-нибудь яркой деталью. Создайте веб-версию изображения посредством графического редактора, потом обрежьте его, чтобы крупнее выделить деталь, и создайте второе изображение (примерно 480px достаточно).
3. Используйте элемент `<picture>` для работы с художественно оформленной картинкой.
4. Обозначьте несколько разных размеров для этой картинки.
5. Используйте `srcset`/`size` для описания переключения при смене размеров вьюпорта

> [!NOTE]
> Используйте инструменты разработчика, чтобы отследить смену размера, как было описано выше.

## Заключение

Это все для отзывчивых изображений - мы надеемся, вам понравилось играть с этими новыми технологиями. Напомним, что мы здесь обсуждали две различные проблемы:

- **Художественное оформление**: Проблема, при которой вы хотите использовать обрезанные изображения для различных макетов - например, ландшафтное изображение для полных экранов на макете компьютера и портретное изображение, показывающее увеличенный основной объект, для мобильного макета. Всё это может быть решено с помощью {{htmlelement("picture")}} элемента.
- **Переключение разрешений**: Проблема, при которой вы хотите использовать файлы изображений меньшего размера на устройствах с узким экраном, поскольку им не нужны огромные изображения, как на настольных дисплеях, а также дополнительно, что вы хотите использовать изображения разного разрешения для экранов с высокой/низкой плотностью. Эту проблему можно решить с помощью [векторной графики](/ru/docs/Learn/HTML/Multimedia_and_embedding/Adding_vector_graphics_to_the_Web) (SVG изображений), и [`srcset`](/ru/docs/Web/HTML/Element/img#srcset) и [`sizes`](/ru/docs/Web/HTML/Element/img#sizes) атрибуты.

Это так же подводит нас к окончанию целого модуля ["Мультимедиа и встраивание"](/ru/docs/Learn/HTML/Multimedia_and_embedding)! Единственное, что вам осталось сейчас сделать перед тем, как двигаться дальше - это попробовать наше мультимедийное задание и посмотреть, как вы усвоили материал. Веселитесь!

## Посмотрите так же

- [Отличное введение в отзывчивые изображения от Джейсона Григсби](http://blog.cloudfour.com/responsive-images-101-definitions)
- [Отзывчивые изображения: Если вы только меняете разрешения используйте srcset](https://css-tricks.com/responsive-images-youre-just-changing-resolutions-use-srcset/) — включает больше объяснений того,как браузер выбирает,какое изображение использовать
- {{htmlelement("img")}}
- {{htmlelement("picture")}}
- {{htmlelement("source")}}

{{PreviousMenuNext("Learn/HTML/Multimedia_and_embedding/Adding_vector_graphics_to_the_Web", "Learn/HTML/Multimedia_and_embedding/Mozilla_splash_page", "Learn/HTML/Multimedia_and_embedding")}}