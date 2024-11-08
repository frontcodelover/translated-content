---
title: Миксин
slug: Glossary/Mixin
---

{{GlossarySidebar}}

Миксин (дословно: "примесь) - класс ({{Glossary("class")}}) или интерфейс, в котором некоторые или все его методы ({{Glossary("method", "methods")}}) и/или свойства ({{Glossary("property", "properties")}}) не реализованы, требуя, чтобы другой класс или интерфейс обеспечивал недостающие реализации. Новый класс или интерфейс затем включает в себя как свойства и методы из миксина, так и те, которые он определяет сам. Все методы и свойства используются совершенно одинаково, независимо от того, реализованы ли они в миксине, интерфейсе или классе, реализующем миксин.

Преимущество миксинов заключается в том, что они могут быть использованы для упрощения проектирования API, в которых несколько интерфейсов должны включать одни и те же методы и свойства.

Например, миксин `WindowOrWorkerGlobalScope` используется для предоставления методов и свойств, которые должны быть доступны как в интерфейсах {{domxref("Window")}}, так и в интерфейсах {{domxref("WorkerGlobalScope")}}. Миксин осуществляется с помощью обоих этих интерфейсов.

## Узнать больше

### General knowledge

- [Mixin](http://en.wikipedia.org/wiki/Mixin) on Wikipedia