---
{"dg-publish":true,"permalink":"/notes/organize-resource-pkm-dendron-workflow/","title":"Dendron Workflow"}
---


## Ресурсы

Нашел такое описание workflow для работы с PKM:
#source/link <https://mstempl.netlify.app/post/pkm-websites/>.
Чел использует несколько инструментов для ведения PKM

- Захватывает новые статьи через [[notes/organize.resource.pkm.app.omnivore\|Omnivore]]
- Редактирует в [[notes/organize.resource.pkm.app.logseq\|Logseq]]
- Управление ссылками в [[notes/organize.resource.pkm.app.nb\|nb]]

## Поиск по заметкам

В Cookbook есть такая идея:
#source/link <https://wiki.dendron.so/notes/401c5889-20ae-4b3a-8468-269def4b4865/#analyze-notes-using-elasticsearch>

Идея заключается в том, чтобы использовать экспорт из dendron в JSON и импортировать результат в [[notes/organize.resource.it.db.elasticsearch\|Elasticsearch]], чтобы искать по заметкам.

Можно подумать на тему того, что еще можно делать с JSON экспортом и импортом, раз есть такая возможность. Мне кажется это главный момент, за который можно зацепиться при разработке прикладных программ на основе dendron.
