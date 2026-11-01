# Neverlose Lua API

Документация Lua API для нашей сборки CS2: события, меню, отрисовка,
игровые объекты и вспомогательные модули.

[Быстрый старт](docs/getting-started.md) · [Полный справочник](docs/reference.md) · [Примеры](examples/README.md)

## Первый скрипт

Создай скрипт через **Extensions → +**, вставь код и нажми **Save & Reload**:

```lua
print("Hello from Neverlose Lua!")

events.on("paint", function()
    render.text(24, 90, color(255, 255, 255), "Hello, Lua!")
end)
```

Готовые примеры можно положить в `C:\neverwin\scripts` и загрузить через
Extensions. Это действующий путь текущей сборки; имя каталога не переименовывалось.

## Разделы API

| Раздел | Что внутри |
| --- | --- |
| [Окружение](docs/reference.md#environment) | LuaJIT, песочница, пути и допустимые контексты |
| [События](docs/reference.md#events) | `paint`, `menu_toggled`, игровые события и отписка |
| [Типы](docs/reference.md#types) | `vector`, `color`, расширения `math`, `json`, `db` |
| [Entity](docs/reference.md#entity) | Игроки, оружие и свойства объектов |
| [Render](docs/reference.md#render) | Текст, фигуры, изображения, шрифты и масштаб |
| [Trace](docs/reference.md#trace) | Линии, объёмы и результаты трассировок |
| [UI](docs/reference.md#ui) | Вкладки, группы, элементы и обращения к меню |
| [Engine и globals](docs/reference.md#engine) | Состояние игры, время и ввод |
| [Client и config](docs/reference.md#client) | Профиль, сообщения, настройки и бинды |
| [Команды и камера](docs/reference.md#cmd) | Контекст `createmove` и [override_view](docs/reference.md#view) |
| [Particle и ESP](docs/reference.md#particle) | Частицы и [элементы ESP](docs/reference.md#esp) |
| [Utils](docs/reference.md#utils) | Кодировки, хеши и время |
| [Insecure API](docs/reference.md#insecure) | Возможности, требующие Allow Insecure |

## Как читать справочник

В обычных скриптах используются Lua-имена функций, а не адреса из бинарника.
Знак `?` у аргумента означает, что он необязательный; `(?)` отмечает детали,
которые ещё требуют проверки. Основа справочника получена реверсом и передана
владельцем проекта; совместимость каждого метода с каждой сборкой не проверялась.

## Сообщить о проблеме

Создай [Issue](https://github.com/PbLJk/neverlose-lua-api/issues) и приложи
минимальный пример, версию сборки, текст ошибки и ожидаемый результат.
