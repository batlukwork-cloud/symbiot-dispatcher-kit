---
doc_class: D4_WORKDOC
doc_code: D4_WORKDOC-SYM-DISP-ШАБЛОН_DISPATCHER_RUN_LOG
version: 1.0
status: template
created: 2026-08-10
updated: 2026-09-28
layer: 2_operation_dispatch
owner: sym_dispatcher
---

# Шаблон Dispatcher Run Log (план → факт)

Связи: `D0_RULE-SYM-DISP-ИНСТРУКЦИЯ_sym_dispatcher_ВЫДАЧА_ОТЧЁТА`, `D0_RULE-SYM-DISP-ИНСТРУКЦИЯ_sym_dispatcher_ЗАПУСК_МИССИИ`, `D2_ARCH-SYM-DISP-CLIENT_ROUTING_REGISTRY`, `D2_ARCH-SYM-DISP-MISSION_TYPE_REGISTRY`.

## 1. Сводка прогона

```text
Диспетчер: симбиот · прогон <run_id> · <дата время>
Сканировано заявок: <N>
  └ опознано и направлено: <X>
  └ на опознании (нужен владелец продукта): <Y>
```

## 2. Карточки заявок (план → факт)

По каждой заявке:

```text
[SIG-XXXXX] <имя заявки>
  Миссия:       <mission_type> · клиент <client_id>
  План:         <что планировалось: куда и как направить>
  Факт:         <ROUTED / GATE / SKIP_PERSONAL / ERROR>
  Как проверено: <адрес / размер / причина — чем подтверждён факт>
```

## 3. Как проверялся результат

```text
Проверка результата:
  [SIG-XXXXX] — папка/файл существует по адресу <путь>, размер <N> байт
  [SIG-YYYYY] — содержимое скопировано, мусорные каталоги отброшены
  [SIG-ZZZZZ] — gate: причина «<причина>», ждёт решения человека
```

## 4. Проверка gates (на каждый сигнал, только если есть непройденные)

| Gate | Статус | Решение |
|---|---|---|
| CLIENT_IDENTIFICATION_GATE | 🛑 | клиент не определён по имени |

## 5. Ссылки и документы (полные адреса)

```text
Документы и источники:
  Реестр клиентов:       <полный путь к 03_РЕЕСТР_КЛИЕНТОВ.md>
  Реестр миссий:         <полный путь к MISSION_TYPE_REGISTRY>
  Карточка миссии (MCC): <полный путь к MCC>
  Итоговый отчёт:        <полный путь к DISPATCHER_RUN_LOG.md>
  Сводка Excel/CSV:      <полный путь к DISPATCHER_SUMMARY>
  Целевая папка клиента: <полный путь к папке клиента>
```
