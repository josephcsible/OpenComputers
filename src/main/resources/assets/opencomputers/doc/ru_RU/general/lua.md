# Lua

Для знакомства с языком Lua и стандартными библиотеками полезно прочитать [справочное руководство по Lua](http://www.lua.org/manual/5.2/manual.html) и книгу ["Программирование на Lua"](http://www.lua.org/pil/) (первое издание доступно бесплатно). [OpenOS](openOS.md) стремится близко соответствовать стандартным библиотекам с несколькими различиями, например в библиотеке debug. Эти различия [документированы в wiki](http://ocdoc.cil.li/api:non-standard-lua-libs).

Нестандартные библиотеки должны быть подключены с помощью `require`, чтобы использовать их в программах. Например:

`local component = require("component")`
`local rs = component.redstone`

Это позволит вызывать функции [платы на красном камне](../item/redstoneCard1.md). К примеру:

`rs.setOutput(require("sides").front, 15)`

**Важно**: при работе с интерпретатором Lua *не используйте* `local`, так как это сделает переменные локальными для одной строки. То есть если вы напишете подряд строки выше, третья строка выдаст ошибку о том, что `rs` имеет значение `nil`. Почему только на третьей строке? Потому что для простоты тестирования интерпретатор пытается загрузить неизвестные переменные как библиотеки. Поэтому, несмотря на то, что после выполнения первой строки ничего не произойдет, использование `component` на второй строке загрузит эту библиотеку. Библиотеки не подгружаются автоматически в программах для экономии памяти.

OpenOS предоставляет множество дополнительных библиотек для написания разных программ, начиная от контроля и управления компонентами [компьютера](computer.md) и заканчивая библиотеками с кодами цветов многожильных проводов, а также кодами клавиш [клавиатуры](../block/keyboard.md). Эти библиотеки можно использовать в программе с помощью функции `require()`, как показано выше. Некоторые библиотеки требуют определенные компоненты для работы, например библиотека `internet` требует [интернет карту](../item/internetCard.md).
