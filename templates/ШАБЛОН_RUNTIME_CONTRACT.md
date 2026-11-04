---
doc_class: D4_WORKDOC
doc_code: D4_WORKDOC-SYM-DISP-ШАБЛОН_RUNTIME_CONTRACT
version: 0.1
status: template
created: 2026-08-10
layer: 2_operation_dispatch
owner: sym_dispatcher
---

# Шаблон Runtime Contract

Связи: `D0_RULE-SYM-DISP-ИНСТРУКЦИЯ_sym_dispatcher_ЗАПУСК_МИССИИ`, `D2_ARCH-SYM-DISP-00_КАРТА_БАЗ_ДИСПЕТЧЕРА`, `D2_ARCH-SYM-DISP-MISSION_TYPE_REGISTRY`, `D2_ARCH-SYM-DISP-AGENT_LAYER_REGISTRY`, `D2_ARCH-SYM-DISP-PRODUCT_REGISTRY`, `D2_ARCH-SYM-DISP-TOOL_REGISTRY`, `D2_ARCH-SYM-DISP-RULE_INDEX`.

## Паспорт

```yaml
runtime_contract_id:
mcc_id:
signal_id:
client_id:
project_id:
mission_type:
mode: R/G/БРОСОК
created_at:
owner_layer_2: sym_dispatcher
executor_layer_3:
validator_agent:
status: draft|ready_for_handoff|in_execution|returned|accepted|closed
```

## 1. Вход

| Поле | Значение |
|---|---|
| `source_id` |  |
| `adapter_id` |  |
| `connector_status` |  |
| `signal_card_path` |  |
| `client_folder` |  |
| `incoming_files` |  |
| `input_summary` |  |

## 2. Цель миссии

```text
Что нужно получить:

Зачем это нужно клиенту:

Что не входит в миссию:
```

## 3. Rule Pack

| Правило | Зачем нужно | Статус |
|---|---|---|
| `D2_ARCH-SYM-DISP-RULE_INDEX` | Проверка обязательных правил миссии. | required |

## 4. Reference Pack

| Источник | Путь/ссылка | Роль в миссии |
|---|---|---|
| Signal Card |  | Исходный запрос. |
| Client Folder |  | Рабочая зона клиента. |
| Mission Control Card |  | Управление миссией. |

## 5. Product Pack

| Поле | Значение |
|---|---|
| Реестр продуктов | `<рабочая папка> |
| Связанные продукты |  |
| Мастер-пути |  |
| Решение | `use_existing_product` / `new_product_gate` / `product_not_required` |
| Ограничение | Новый продукт создается только в `<рабочая папка> дубли вне корня запрещены. |

Исполнитель обязан прочитать Product Pack до начала работы. Если указанный мастер-путь отсутствует или найден конкурирующий контур, задача возвращается Диспетчеру.

## 6. Agent Pack

| Роль | Агент | Слой | Ответственность |
|---|---|---|---|
| owner | sym_dispatcher | 2 | Маршрутизация и контроль контракта. |
| executor |  | 3 | Исполнение результата. |
| validator |  | 2/3 | Проверка evidence и acceptance. |

## 7. Tool Pack

| Инструмент | Статус | Разрешенное действие | Ограничение |
|---|---|---|---|
|  |  |  |  |

## 8. Output Contract

| Артефакт | Куда положить | Формат | Кто проверяет |
|---|---|---|---|
| Основной результат |  |  |  |
| Evidence |  |  |  |
| Краткий отчет |  | md/text | sym_dispatcher |

## 9. Stop Conditions

Исполнитель обязан вернуть задачу диспетчеру, если:

- входные данные противоречат друг другу;
- нужен новый источник истины;
- нужен инструмент вне Tool Pack;
- нужен новый агент;
- нужен новый продукт или не найден мастер-контур продукта;
- цель миссии изменилась;
- результат затрагивает деньги, право, публичное обещание, клиентские данные или необратимые действия сверх контракта.

## 10. Acceptance Criteria

```text
1.
2.
3.
```

## 11. Runtime Handoff

```text
Передал:
Принял:
Дата/время:
Канал:
Следующий gate:
```
