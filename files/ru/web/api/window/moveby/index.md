---
title: Window.moveBy()
slug: Web/API/Window/moveBy
---

{{APIRef}}

Метод **`moveBy()`** интерфейса [`Window`](/ru/docs/Web/API/Window) перемещает текущее окно на указанное количество.

> [!NOTE]
> Эта функция перемещает окно относительно текущего положения. В свою очередь, {{domxref("window.moveTo()")}} перемещает к абсолютному значению.

## Синтаксис

```
window.moveBy(deltaX, deltaY)
```

### Параметры

- `deltaX` количество пикселей, на которое будет перемещено окно по горизонтали. Положительное значение перемещает вправо, а отрицательное перемещает влево.
- `deltaY` количество пикселей, на которое будет перемещено окно по вертикали. Положительное значение перемещает вниз, а отрицательное перемещает вверх.

## Пример

Этот пример перемещает окно на 10 пикселей вправо и на 10 пикселей вверх.

```js
function budge() {
  moveBy(10, -10);
}
```

## Спецификации

{{Specifications}}

## Совместимость с браузерами

{{Compat}}

Начиная с Firefox 7 сайты не могут перемещать окно [в следующих случаях](https://bugzilla.mozilla.org/show_bug.cgi?id=565541#c24):

1. Вы не можете переместить окно или вкладку, которое было создано не с помощью{{domxref("Window.open()")}}.
2. Вы не можете переместить окно или вкладку, когда окно имеет более одной вкладки.

## Смотрите также

- {{domxref("Window.moveTo()")}}