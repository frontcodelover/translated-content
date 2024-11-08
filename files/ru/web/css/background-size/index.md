---
title: background-size
slug: Web/CSS/background-size
---

{{CSSRef}}

## Описание

Значение **`background-size`** в [CSS](/ru/docs/CSS) позволяет задавать размер фонового изображения. Изображение может быть оставлено в исходном размере, растянуто, или подогнано под размеры доступного пространства.

> [!NOTE]
> Если значение этого свойства не задано в сокращённом свойстве {{cssxref("background")}}, которое применяется к элементу после CSS-свойства `background-size`, то значение этого свойства затем сбрасывается до исходного значения c помощью сокращённого свойства.

{{cssinfo}}

## Синтаксис

```css
/* Ключевые слова */
background-size: cover;
background-size: contain;

/* Указано одно значение - ширина изображения, */
/* высота в таком случае устанавливается в auto */
background-size: 50%;
background-size: 3em;
background-size: 12px;
background-size: auto;

/* Указаны два значения - */
/* ширина и высота соответственно */
background-size: 50% auto;
background-size: 3em 25%;
background-size: auto 6px;
background-size: auto auto;

/* Значения для нескольких фонов */
/* Не путайте такую запись с background-size: auto auto */
background-size: auto, auto;
background-size: 50%, 25%, 25%;
background-size: 6px, auto, contain;

/* Глобальные значения */
background-size: inherit;
background-size: initial;
background-size: unset;
```

### Значения

- `<размер>`
  - : Значение `{{cssxref("&lt;length&gt;")}}` позволяет масштабировать размер фонового изображения в заданном измерении. Отрицательный размер не допускается.
- `<проценты>`
  - : Значение `{{cssxref("&lt;percentage&gt;")}}`, которое масштабирует фоновое изображение в соответствующем измерении до указанного процента области расположения фона, которое определяется значением {{cssxref("background-origin")}}. Область расположения фона по умолчанию является областью, содержащей содержимое поля и его отступы; область также может быть изменена на содержимое или область, содержащую границы, отступы и содержимое. Если {{cssxref("background-attachment","attachment")}} фона является `fixed`, область позиционирования фона вместо этого является всей областью окна браузера, не включая область, покрытую полосами прокрутки, если они присутствуют. Отрицательные проценты не допускаются.
- `auto`
  - : Значение позволяет изменять размер фонового изображения в соответствии с заданным направлением, сохраняя его пропорции.
- `contain`
  - : Масштабирует картинку так, чтобы она максимально накрыла собой весь блок. Картинка при этом не обрезается, а вписывается в блок с сохранением пропорций.
- `cover`
  - : Ключевое слово, обратное `contain`. Масштабирует изображение как можно больше c сохранением пропорций изображения (изображение не становится сплющенным). Когда изображение и контейнер имеют разные размеры, _изображение обрезается_ либо влево / вправо, либо сверху / снизу.

Интерпретация возможных значений зависит от внутренних размеров изображений (ширина и высота) и внутренней пропорции (соотношение ширины и высоты). Растровое изображение всегда имеет внутренние размеры и внутреннюю пропорцию. Векторное изображение может иметь оба внутренних размера (и, следовательно, должно иметь внутреннюю пропорцию). Он также может иметь одно или не иметь внутренних размеров, и в любом случае он может иметь или не иметь внутреннюю пропорцию. Градиенты обрабатываются как изображения без внутренних размеров или внутренней пропорции.

> [!WARNING]
> Это поведение изменилось в Gecko 8.0. До этого, градиенты обрабатывались как изображения без внутренних размеров, с внутренней пропорцией, идентичной пропорции области расположения фона.

Фоновые изображения, сгенерированные из элементов с использованием {{cssxref("-moz-element")}} (которые фактически соответствуют элементу) в настоящее время обрабатываются как изображения с размерами элемента, или как область расположения фона, если элементом является SVG, с соответствующей внутренней пропорцией.

> [!WARNING]
> Это не определённое в настоящее время поведение, которое заключается в том, что внутренние размеры и пропорция должны быть такими же как у элемента во всех случаях.

Визуализированный размер фонового изображения затем вычисляется следующим способом:

- Если оба атрибута в `background-size` заданы и различны от `auto`:
  - : Фоновое изображение отображается в указанном размере.
- Если `background-size` содержит `contain` или `cover`:
  - : Изображение визуализируется с сохранением его внутренней пропорции при наибольшем размере, который содержится внутри области размещения фона или покрывает её. Если изображение не имеет внутренней пропорции, оно отображается с размером области расположения фона.
- Если `background-size` установлен как `auto` или `auto auto`:
  - : Если изображение имеет оба внутренних размера, оно отображается с таким размером. Если оно не имеет внутренних размеров и внутренней пропорции, оно отображается с размером области расположения фона. Если оно не имеет размеров, но имеет пропорцию, оно отображается так, если был был бы указан `contain`. Если изображение имеет один внутренний размер и пропорцию, оно отображается с размером, определённым этим одним размером и пропорцией. Если изображение имеет один внутренний размер, но не имеет пропорцию, оно отображается с использованием внутреннего размера и соответствующим размером области позиционирования фона.
- Если background-size содержит один атрибут `auto` и один не-`auto`:
  - : Если изображение имеет внутреннюю пропорцию, то визуализируйте его используя указанный размер, и вычислите другой размер из указанного размера и внутренней пропорции. Если изображение не имеет внутренней пропорции, используйте указанный размер для этого размера. Для другого размера, используйте соответствующее внутреннее измерение изображения, если оно есть. Если такого внутреннего размера нет, используйте соответствующий размер области расположения фона.

Обратите внимание, что изменение размера фона для векторных изображений, в которых отсутствуют внутренние размеры или пропорции, ещё не полностью реализовано во всех браузерах. Будьте осторожны, полагаясь на поведение, описанное выше, и тестируйте в нескольких браузерах (в частности, включая версии Firefox 7 или более ранней версии и Firefox 8 или более поздней версии), чтобы убедиться, что различные визуализации приемлемы.

### Формальный синтаксис

{{csssyntax}}

## Примеры

[Эта демонстрация `background-size: cover`](http://whereswalden.com/files/mozilla/background-size/page-cover.html) и [эта демонстрация `background-size: contain`](http://whereswalden.com/files/mozilla/background-size/page-contain.html) предназначены для открытия в новых окнах, чтобы вы могли видеть, как `contain` и `cover` ведут себя, когда размеры области расположения фона изменяются. [Эта серия демонстраций, как работает `background-size` и взаимодействует с другими свойствами `background-*`](http://whereswalden.com/files/mozilla/background-size/more-examples.html), должна в значительной степени охватить оставшуюся основу в том, как использовать `background-size` отдельно и в сочетании с другими свойствами.

## Замечания

Если вы указываете градиент в качестве фона и указали `background-size`, который будет использоваться вместе с ним, лучше не указывать размер, который использует единственную автоматическую составную часть, или задаётся с использованием только значения ширины (для примера, `background-size: 50%`). Рендеринг градиентов в таких случаях изменился в Firefox 8, и в настоящее время он обычно несовместим во всех браузерах, которые не реализуют рендеринг в соответствии с [CSS3 спецификацией `background-size`](http://www.w3.org/TR/css3-background/#the-background-size) и с [CSS3 спецификацией градиента значений изображения](http://dev.w3.org/csswg/css3-images/#gradients).

```css
.bar {
  width: 50px;
  height: 100px;
  background-image: gradient(...);

  /* Лучше не использовать */
  background-size: 25px;
  background-size: 50%;
  background-size: auto 50px;
  background-size: auto 50%;

  /* Допускается */
  background-size: 25px 50px;
  background-size: 50% 50%;
}
```

Обратите внимание, что особенно не рекомендуется использовать размер в пикселях и размер `auto` с градиентом, потому что невозможно воспроизвести рендеринг в версиях Firefox до 8 и в браузерах, не реализующих рендеринг Firefox 8, без знания точного размера элемента, фон которого указывается.

## Спецификации

{{Specifications}}

## Совместимость с браузерами

{{Compat}}

## Смотрите также

- [Справочник по CSS](/ru/docs/CSS/CSS_Reference)
- [Несколько фонов](/ru/docs/CSS/Multiple_backgrounds)
- [Масштабирование фонового изображения](/ru/docs/CSS/Scaling_background_images)