---
title: Научитесь стилизовать HTML с помощью CSS
slug: Learn/CSS
---

{{LearnSidebar}}

Каскадные таблицы стилей — или {{glossary("CSS")}} — это технология, которую следует изучать непосредственно после HTML. В отличие от HTML, который служит для определения структуры и семантики содержимого, CSS отвечает за его внешний вид и отображение. К примеру, с помощью CSS можно изменять шрифт, цвет, размер, межстрочный интервал, разделять содержимое на колонки, а также добавлять анимацию и другие декоративные элементы.

> [!CALLOUT]
>
> #### Хотите стать frontend-разработчиком?
>
> Мы составили курс, который содержит всю необходимую информацию для достижения этой цели.
>
> [**Начать изучение курса**](/ru/docs/Learn/Front-end_web_developer)

## Необходимые условия

Прежде чем браться за CSS, вам стоит разобраться с основами HTML. Мы рекомендуем сначала изучить модуль [Введение в HTML](/ru/docs/Learn/HTML/Introduction_to_HTML)

После того как вы разберётесь с основами HTML, мы рекомендуем продолжать изучение HTML и CSS одновременно, переключаясь между темами. HTML гораздо интереснее в сочетании с CSS, и вы не можете по настоящему изучить CSS не зная HTML

В данном разделе содержится информация, которая требует базового знакомства с компьютером и интернетом. В статье [Установка рабочего пространства](/ru/docs/Learn/Getting_started_with_the_web/Installing_basic_software) подробно описано необходимое ПО и способы его установки, необходимо также будет уметь создавать и управлять файлами, в чём поможет статья [Работа с файлами](/ru/docs/Learn/Getting_started_with_the_web/Dealing_with_files), которая включена в полное руководство для новичка [Основы веб](/ru/docs/Learn/Getting_started_with_the_web).

Перед тем как начинать данный раздел, мы рекомендуем пройти руководство [Основы веб](/ru/docs/Learn/Getting_started_with_the_web), хотя это вовсе не обязательно — большая часть того, что вы найдёте в статье об основах CSS также встречается в разделе [Введение в CSS](/ru/docs/Learn/CSS/First_steps), хотя и более детально.

## Модули

Этот раздел содержит модули в порядке, наиболее подходящем для работы с ними. Лучше всего начать с самого первого.

- [Введение в CSS](/ru/docs/Learn/CSS/First_steps)
  - : CSS (каскадные таблицы стилей) используется для стилизации и компоновки веб-страниц — например, для изменения шрифта, цвета, размера и интервала содержимого, разделения его на несколько столбцов или добавления анимации и других декоративных элементов. Этот модуль обеспечивает хорошее начало вашего пути к освоению CSS с основами того, как он работает, как выглядит синтаксис и как вы можете начать использовать его для добавления стилей в HTML.
- [Устройство CSS](/ru/docs/Learn/CSS/Building_blocks)

  - : Этот модуль продолжается с того места, где закончился модуль [введение в CSS](/ru/docs/Learn/CSS/First_steps) — теперь, после того как вы познакомились с языком и получили опыт его использования, пришло время погрузится немного глубже. В этот модуле рассказывается про каскад и наследование, все доступные типы селекторов, единицы измерения, размеры, стилизацию фона и рамок, отладку, и многое другое.

    Цель этого модуля — предоставить вам инструментарий для написания компетентного CSS, перед переходом к более специфичным дисциплинам, как [стилизация текста](/ru/docs/Learn/CSS/Styling_text) и [CSS раскладки](/ru/docs/Learn/CSS/CSS_layout).

- [Стилизация текста](/ru/docs/Learn/CSS/Styling_text)
  - : После изучения основ, следующая тема, которую стоит изучить — стилизация текста. Это одна из самых распространенных вещей, для которых используется CSS. В этом модуле мы рассмотрим основы стилизации текста, включая установку шрифта, жирность, курсив, межстрочный и межбуквенный интервалы, тени и другие особенности оформления. В завершении модуля мы рассмотрим подключение пользовательских шрифтов на странице, а так же стилизацию списков и ссылок
- [CSS раскладки](/ru/docs/Learn/CSS/CSS_layout)
  - : К текущему моменту мы познакомились с основами CSS. Мы знаем, как оформлять текст, как оформлять и изменять блоки, в которых находится ваш контент. Пришло время узнать, как разместить ваши блоки в нужных местах в зависимости от области просмотра и тому подобного. Мы уже знаем достаточно, чтобы погрузиться в изучение раскладки с помощью CSS, в то, как изменять отображение в зависимости от особенностей экрана, как использовать современные методы раскладки, такие как Flexbox и CSS grid, и некоторые традиционные методы раскладки, которые все ещё применяются.

## Решаем часто встречающиеся проблемы в CSS

В разделе **[Использование CSS для решения общих проблем](/ru/docs/Learn/CSS/Howto)** даны ссылки на разделы, объясняющие, как следует использовать CSS для решения самых распространённых проблем при создании веб-страницы.

В самом начале вы будете применять цвет к тексту и фону HTML-элементов, изменять их размер, форму, местоположение, добавлять и стилизовать границы. Однако с углублённым знанием даже основ CSS вы сможете сделать практически что угодно. Одним из плюсов изучения CSS является то, что вы быстро начнёте понимать, можно или нельзя что-то сделать средствами CSS, даже если вы ещё не уверены, как это сделать.

## "CSS странный"

CSS иначе, чем большинство языков программирования и инструментов для дизайна, с которыми вы можете столкнуться. Почему это работает именно так? В следующем видео, Мириам Сюзанна дает объяснение того, почему CSS работает так, как он работает, и почему он так развивался:

{{EmbedYouTube("aHUtMbJw8iA")}}

## Смотрите также

- [CSS на MDN](/ru/docs/Web/CSS)
  - : Основная точка входа для CSS документации на MDN, где вы найдете вы найдете справочную информацию по функциям языка CSS. Хотите знать все значения, которые может принимать какое-либо свойство? Тогда вам сюда