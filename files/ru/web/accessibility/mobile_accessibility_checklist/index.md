---
title: Контрольный список по мобильной доступности
slug: Web/Accessibility/Mobile_accessibility_checklist
---

{{AccessibilitySidebar}}

Этот документ содержит краткий список требований доступности для разработчиков мобильных приложений. Он будет обновляться по мере появления новых техник и подходов.

## Цвет

- Контраст цвета **ДОЛЖЕН** соответствовать требованиям уровня AA [WCAG 2.0](http://www.w3.org/TR/WCAG/):

  - Коэффициент контрастности 4.5:1 для обычного текста (менее 18 пунктов или 14 пунктов для жирного текста).
  - Коэффициент контрастности 3:1 для крупного текста (минимум 18 пунктов или 14 пунктов для жирного текста).

- Информация, передаваемая через цвет, **ДОЛЖНА** быть доступна и другими способами (подчёркнутый текст для ссылок и т. д.).

## Видимость

- Техники сокрытия содержимого, такие как нулевая непрозрачность, порядок z-индекса и размещение вне экрана, **НЕ ДОЛЖНЫ** использоваться исключительно для управления видимостью.
- Всё, кроме видимого в данный момент экрана, **ДОЛЖНО** быть действительно невидимым:

  - **ИСПОЛЬЗУЙТЕ** `hidden` **атрибут или свойство** **`visibility`** или изменяйте тип отображения.
  - Без абсолютной необходимости, **НЕ ИСПОЛЬЗУЙТЕ** `aria-hidden` атрибут.

## Фокус

- Все интерактивные элементы **ДОЛЖНЫ** иметь состояние фокуса:

  - Стандартные элементы, такие как ссылки, кнопки и поля формы фокусируемые по умолчанию.
  - Нестандартные элементы **ДОЛЖНЫ** иметь соответствующую [ARIA-роль](http://www.w3.org/TR/wai-aria/roles), назначенную им. Например, кнопка, ссылка или чекбокс.

- Фокус должен обрабатываться в логическом порядке и последовательным образом.

## Текстовые эквиваленты

- Текстовый эквивалент **ДОЛЖЕН** быть предусмотрен для каждого не строго презентационного нетекстового элемента в приложении.

  - Используйте _alt_ и _title_ там, где это уместно ([см. статью](http://blog.paciellogroup.com/2013/01/using-the-html-title-attribute-updated/) Steve Faulkner's про использование HTML атрибута {{ htmlelement("title") }}).
  - Если вышеуказанные атрибуты неприменимы, используйте соответствующие [ARIA-свойства](http://www.w3.org/WAI/PF/aria/states_and_properties#global_states_header), такие как `aria-label`, `aria-labelledby`, или `aria-describedby`.

- Необходимо **ИЗБЕГАТЬ** текста внутри изображений.
- Все элементы формы **ДОЛЖНЫ** иметь метки ({{ htmlelement("label") }} элементы) в интересах пользователей программы чтения с экрана.

## Обработка состояния

- Стандартные элементы, такие как радиокнопки и чекбоксы обрабатываются операционной системой. Однако, для других кастомных элементов изменения состояния должны быть предоставлены через [ARIA-состояния](http://www.w3.org/TR/wai-aria/states_and_properties#attrs_widgets_header), такие как `aria-checked`, `aria-disabled`, `aria-selected`, `aria-expanded`, and `aria-pressed`.

## Общие рекомендации

- **ДОЛЖНО** быть указано название приложения ({{ htmlelement("title") }} элемент).
- Заголовки **НЕ ДОЛЖНЫ** нарушать иерархическую структуру.

  ```html
  <h1>Заголовок верхнего уровня</h1>
  <h2>Вторичный заголовок</h2>
  <h2>Другой вторичный заголовок</h2>
  <h3>Заголовок низкого уровня</h3>
  ```

- [ARIA Landmark Roles](http://www.w3.org/TR/wai-aria/roles#landmark_roles_header) **СЛЕДУЕТ** использовать для описания приложения или структуры документа, такие как `banner`, `complementary`, `contentinfo`, `main`, `navigation`, `search`.
- Обработчики сенсорных событий **ДОЛЖНЫ** запускаться только при соответствующих событиях.
- Области нажатия **ДОЛЖНЫ** быть достаточно большими, чтобы пользователь мог взаимодействовать с ними (см. статью [BBC Mobile Accessibility Guidelines](http://www.bbc.co.uk/guidelines/futuremedia/accessibility/mobile/design/touch-target-size) с полезными рекомендациями по размеру области нажатия для сенсорного объекта).

> [!NOTE] > [Исходную версию этого документа](http://yzen.github.io/firefoxos/2014/04/30/mobile-accessibility-checklist.html) написал [Юра Зеневич](http://yzen.github.io/).