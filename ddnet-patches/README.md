# Фиксы для DDNet

17 патчей для [ddnet/ddnet](https://github.com/ddnet/ddnet), по одному коммиту на фикс, все поверх master `f396f2870` (24.09.2026).

Каждый фикс:
- воспроизведён на master;
- собран в Debug с `-Werror`, как в CI;
- прогнан через `testrunner`: из 366 тестов падает только `Net.Ipv4AndIpv6Work`, потому что в контейнере нет IPv6, на master так же;
- проверен clang-format 20 и стилевыми скриптами из CI;
- проверен в игре под Xvfb или юнит-тестом;
- прошёл независимое ревью.

## Порядок

| Уровень | Патч | Что чинит |
|---|---|---|
| начать | `10852-editor-tunezone-setting-replace.patch` | Правка tune_zone в редакторе удаляет другую настройку (1 строка) |
| начать | `12138-streamer-mode-save-code-localized.patch` | Режим стримера не скрывает код сохранения на других языках |
| начать | `8034-editor-map-settings-quotes.patch` | Редактор считает настройки карты в кавычках ошибкой |
| начать | `8179-chat-preview-wrapping.patch` | Фон сообщения в превью чата не совпадает с текстом (1 строка) |
| начать | `11354-demo-intratick-div-zero.patch` | UB в HUD при перемотке демо, есть тест |
| начать | `fifo-keep-existing.patch` | Сервер удаляет существующий input FIFO, регрессия из #11470, есть тест, issue нет |
| нюансы | `11576-editor-switch-copy-number.patch` | Вставка свитчей меняет номер и задержку тайлов |
| нюансы | `10697-editor-brush-lockup-popup.patch` | Кисть залипает после Ctrl+S / Ctrl+P во время рисования |
| нюансы | `12033-editor-door-preview-collision.patch` | Превью двери в редакторе проходит сквозь стены |
| нюансы | `10577-console-toggle-nan.patch` | NaN-высота консоли при быстром открытии и закрытии |
| нюансы | `8746-console-quote-completion.patch` | Кавычка в консоли ломает подсказки команд |
| нюансы | `12826-console-copy-newlines.patch` | Копирование многострочного вывода rcon сдвигается, пересекается с открытым PR #12416 |
| нюансы | `9843-rcon-log-thread-flush.patch` | Вывод из потоков доходит до rcon/econ с опозданием |
| нюансы | `11504-hud-rank-skin-overlap.patch` | Номер места в HUD налезает на тишку |
| нюансы | `12333-rcon-cmdlist-dummy.patch` | Dummy в rcon видит чужой список команд, фикс частичный |
| спорно | `11154-browser-country-none-twice.patch` | Двойной флаг «без страны», меняет поведение фильтра |
| спорно | `7079-spectator-menu-label-overlap.patch` | Подписи в меню наблюдателя, длинные переводы становятся мелкими |

## Как применить

```sh
git clone https://github.com/<твой-ник>/ddnet && cd ddnet
git checkout -b editor-tunezone-setting-replace
git am /path/to/ddnet-patches/10852-editor-tunezone-setting-replace.patch
```

## Перед PR

- Один PR за раз.
- Описание PR и ответы на ревью пиши сам, своими словами.
- Чекбокс «I didn't use generative AI…» не ставь и в 1–2 предложениях опиши, как использовался ИИ. В коммитах есть трейлер `Co-Authored-By: Claude`.
- Прочитай комментарии в issue на GitHub: при подготовке они были недоступны.
- Проверь фикс в игре сам и приложи скриншоты для визуальных изменений.
