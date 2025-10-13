---
{"dg-publish":true,"permalink":"/notes/organize.resource.it.data-structure.append-only-log/","title":"Append Only Log"}
---


Структура используемая для построения систем основанных на логах и событиях.

Идея Append Only Log заключается в том, что структура иммутабельна, то есть хранит все предыдущие состояния.

Используется при реализации [[notes/organize.resource.it.sysdesign.event-sourcing \| event-sourcing pattern]].