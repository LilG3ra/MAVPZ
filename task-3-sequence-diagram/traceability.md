# Матриця трасування взаємодій — онлайн-книжковий магазин

## Призначення

Цей документ пов'язує функціональні вимоги Завдання №2, Use Case UC-04 «Оформити замовлення», чотири Gherkin-сценарії та відповідні Sequence Diagram Завдання №3. Джерела вимог — [requirements/functional.md](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/requirements/functional.md), [use-cases.md](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/use-cases.md) та [сценарії Gherkin](https://github.com/LilG3ra/MAVPZ/tree/main/task-2-requirements-use-case/scenarios). Вимоги та сценарії повторно не дублюються.

## Зв'язок функціональних вимог із UC-04, Gherkin та Sequence Diagram

| Вимога | Короткий зміст | Use Case | Gherkin-сценарій | Sequence Diagram |
|---|---|---|---|---|
| FR-07 | Оформлення замовлення без реєстрації | UC-04 | UC04-S01 | [SC-01](diagrams/sc-01-success.md) |
| FR-08 | Заборона порожнього замовлення | UC-04 | — | [SC-01](diagrams/sc-01-success.md) — validateItems() |
| FR-09 | Відхилення кількості меншої за 1 | UC-04 | UC04-S03 | [SC-03](diagrams/sc-03-invalid-quantity.md) |
| FR-10 | Перевірка складського залишку | UC-04 | UC04-S01, UC04-S02 | [SC-01](diagrams/sc-01-success.md), [SC-02](diagrams/sc-02-insufficient-stock.md) |
| FR-11 | Відхилення замовлення за нестачі примірників | UC-04 | UC04-S02 | [SC-02](diagrams/sc-02-insufficient-stock.md) |
| FR-12 | Перевірка обов'язкових контактних даних | UC-04 | UC04-S04 | [SC-04](diagrams/sc-04-missing-contacts.md) |
| FR-13 | Створення ORDER та ORDER_ITEM | UC-04 | UC04-S01 | [SC-01](diagrams/sc-01-success.md) |
| FR-14 | Фіксація ціни та обчислення суми позиції | UC-04 | UC04-S01 | [SC-01](diagrams/sc-01-success.md) — фіксація ціни показана; обчислення суми окремо не відображено |
| FR-15 | Підтвердження успішного оформлення | UC-04 | UC04-S01 | [SC-01](diagrams/sc-01-success.md) |

## Покриття Gherkin-сценаріїв UC-04

- **UC04-S01 — успішне оформлення:** FR-07, FR-10, FR-13, FR-14, FR-15 → [SC-01](diagrams/sc-01-success.md). Додатково SC-01 відображає перевірку FR-08, хоча окремого Gherkin-сценарію для неї в матриці Завдання №2 немає.
- **UC04-S02 — недостатньо примірників:** FR-10, FR-11 → [SC-02](diagrams/sc-02-insufficient-stock.md).
- **UC04-S03 — некоректна кількість:** FR-09 → [SC-03](diagrams/sc-03-invalid-quantity.md).
- **UC04-S04 — відсутні обов'язкові контакти:** FR-12 → [SC-04](diagrams/sc-04-missing-contacts.md).

## Узгодженість з ER-моделлю Завдання №1

| Діаграма | Сутності та їхня роль |
|---|---|
| SC-01 | **EDITION** — перевірка залишку й отримання актуальної ціни; **ORDER** — створення замовлення; **ORDER_ITEM** — створення позицій із кількістю та зафіксованою ціною |
| SC-02 | **EDITION** — читання доступного залишку; **ORDER** і **ORDER_ITEM** не створюються |
| SC-03 | **EDITION** — ідентифікатор вибраного видання у вхідних даних; звернення до сховища й створення замовлення немає |
| SC-04 | Контактні дані покупця перевіряються без звернення до сховища; **ORDER** і **ORDER_ITEM** не створюються; реєстрація **USER** не вимагається |

## Висновок

У Завданні №3 створено чотири Sequence Diagram для всіх чотирьох Gherkin-сценаріїв UC-04. Вони деталізують успішне оформлення замовлення та три причини відмови, зберігаючи зв'язок із вимогами Завдання №2 і предметною областю Завдання №1. Для FR-14 потрібно окремо підтвердити обчислення суми позиції: на SC-01 наразі явно показано лише фіксацію ціни. Дослівну відповідність усіх кроків оригінальним Gherkin-сценаріям слід перевірити перед здачею.
