# Automatic correction of the language for words in the text because of the wrong keyboard layout. Автоматическое исправление языка для слов в тексте из-за неправильной раскладки клавиатуры

## Purpose

1. Корректировка поисковых запросов
1. Корректировка существующих и новых текстов, публикуемых посетителями на веб-сайтах.

## Features

1. Режим `SIMILAR_CHARS`. Исправление ошибочно набранных букв в словах, которые выглядят одинаково в разных раскладках клавиатуры. Незаметные латинские буквы среди русских исправляются в русские и наоборот. Алгоритм работает достаточно надёжно и быстро.
1. Режим `KEYBOARD_LAYOUT`. Исправление ошибочно набранных слов в другой раскладке клавиатуры. Для определения языка используются N-граммы. Алгоритм может иногда ошибаться, работает в разы медленнее, чем SIMILAR_CHARS. Алгоритм постоянно совершенствуется. Для поддержания качества существует тестовый набор слов, который в поставку не входит.
1. Двухстороннее исправление слов для русского и английского языка.
1. Исправление слов на смешанном языке.
1. Кодировка символов — Text\Util\UTF8.
1. Класс может работать без расширений `mbstring` и `iconv`!

Examples

    "\xd1\x81\xd0\xbesm\xd0\xbe" => 'cosmo' (2 первых и последняя буква — ошибочные)
    "\x78\x70\x65н"              => 'хрен'  (первые 3 буквы — ошибочные)
    "вебvfcnth"                  => 'вебмастер'
    "webьфыеук"                  => 'webmaster'
    "цццюмуыеш.ru"               => 'www.vesti.ru'
    "\x54.\x43.\x48\x61вка"      => 'Т.С.Навка'

## Пример работы алгоритма для поля ввода с автодополнением

1. Сделать выборку из БД по исходному запросу;
1. Если есть результат, возвратить его и исходный запрос;
1. Иначе скорректировать исходный запрос через `Text\Text_LangCorrect`;
1. Если исходный и скорректированный запрос совпадает, возвратить пустой результат и исходный запрос;
1. Иначе сделать выборку из БД по скорректированному запросу;
1. Возвратить результат. Если результат не пустой, возвратить скорректированный запрос, иначе исходный.
