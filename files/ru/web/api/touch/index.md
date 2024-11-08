---
title: Touch
slug: Web/API/Touch
---

{{ APIRef("Touch Events") }}

Интерфейс **`Touch`** представляет определённую точку касания на сенсорном устройстве. Точка касания – это место контакта пальца или стилуса с сенсорной поверхностью тачскрина или трекпада.

Свойства {{ domxref("Touch.radiusX") }}, {{ domxref("Touch.radiusY") }}, и {{ domxref("Touch.rotationAngle") }} содержат данные об области контакта между пользователем и экраном – _области касания_. Они могут быть полезны при работе с устройствами, предусматривающими указатели низкой точности, например палец. Эти значения описывают эллипс, который соответствует области контакта (например, кончик пальца пользователя). {{experimental_inline}}

> [!NOTE]
> Многие значения зависят от устройства; например, если устройство не способно измерять силу нажатия на сенсорную поверхность, значение `force` всегда будет равняться 0. То же касается значений `radiusX` и `radiusY`; если у устройства только одна точка касания, данные значения всегда будут равны 1.

## Конструктор

- {{domxref("Touch.Touch", "Touch()")}} {{experimental_inline}}
  - : Создаёт объект Touch.

## Свойства

_Данный интерфейс не имеет предков, не наследует и не реализует другие свойства._

### Основные свойства

- {{ domxref("Touch.identifier") }} {{readonlyInline}}
  - : Возвращает уникальный идентификатор указанного объекта `Touch`. Данная точка касания (например, пальцем) будет иметь один и тот же идентификатор на протяжении всего движения по сенсорной поверхности. Это гарантирует, что вы всё время отслеживаете одно и то же касание.
- **{{ domxref("Touch.screenX") }}** {{readonlyInline}}
  - : Возвращает координату X точки касания относительно левого края экрана.
- **{{ domxref("Touch.screenY") }}** {{readonlyInline}}
  - : Возвращает координату Y точки касания относительно верхнего края экрана.
- **{{ domxref("Touch.clientX") }}** {{readonlyInline}}
  - : Возвращает координату X точки касания относительно левого края окна браузера, не учитывая прокрутку.
- **{{ domxref("Touch.clientY") }}** {{readonlyInline}}
  - : Возвращает координату Y точки касания относительно верхнего края окна браузера, не учитывая прокрутку.
- {{ domxref("Touch.pageX") }} {{readonlyInline}}
  - : Возвращает координату X точки касания относительно левого края документа. В отличие от `clientX`, это значение учитывает горизонтальную прокрутку, если она есть.
- {{ domxref("Touch.pageY") }} {{readonlyInline}}
  - : Возвращает координату Y точки касания относительно верхнего края документа. В отличие от `clientY`, это значение учитывает вертикальную прокрутку, если она есть.
- {{ domxref("Touch.target") }} {{readonlyInline}}
  - : Возвращает элемент ({{ domxref("Element")}}), на который попала точка касания, когда впервые появилась на сенсорной поверхности, даже если потом она была смещена за пределы данного элемента или даже была удалена из документа.

### Область касания

{{SeeCompatTable}}

- {{ domxref("Touch.radiusX") }} {{readonlyInline}} {{experimental_inline}}
  - : Возвращает радиус эллипса по оси X, наиболее близко соответствующий области контакта с экраном. Значение в пикселях того же масштаба, что и `screenX`.
- {{ domxref("Touch.radiusY") }} {{readonlyInline}} {{experimental_inline}}
  - : Возвращает радиус эллипса по оси Y, наиболее близко соответствующий области контакта с экраном. Значение в пикселях того же масштаба, что и `screenY`.
- {{ domxref("Touch.rotationAngle") }} {{readonlyInline}} {{experimental_inline}}
  - : Возвращает угол (в градусах), на который описываемый эллипс должен быть повёрнут по часовой стрелке, чтобы наиболее точно покрыть область контакта пользователя с сенсорной поверхностью.
- {{ domxref("Touch.force") }}{{readonlyInline}} {{experimental_inline}}
  - : Возвращает силу давления пользователем на сенсорную поверхность. Является числом от 0.0 (без давления) до 1.0 (максимальное давление).

## Методы

_Этот интерфейс не имеет метода и родителя, а также не наследует и не реализует какой-либо метод._

## Спецификации

{{Specifications}}

## Совместимость с браузерами

{{Compat}}

## Смотрите также

- {{domxref("Touch_events","Touch Events Overview")}}
- {{ domxref("Document.createTouch()") }}

<!---->