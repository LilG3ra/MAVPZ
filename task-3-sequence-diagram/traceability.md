# Матриця трасування взаємодій — онлайн-книжковий магазин

## Призначення

Цей документ пов'язує функціональні вимоги Завдання №2, сценарій використання UC-04 «Оформити замовлення», сценарії Gherkin та відповідні Sequence Diagram Завдання №3.

Основою є [функціональні вимоги](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/requirements/functional.md), [Use Cases](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/use-cases.md) та [сценарії Gherkin](task-2-requirements-use-case/scenarios/UC-04-order-scenario.md) із Завдання №2.

## Зв'язок функціональних вимог із UC-04, Gherkin та Sequence Diagram

| Вимога | Короткий зміст | Use Case | Gherkin-сценарій | Sequence Diagram |
|---|---|---|---|---|
| FR-07 | Оформлення замовлення без реєстрації | UC-04 | UC04-S01 | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) |
| FR-08 | Заборона порожнього замовлення | UC-04 | — | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) |
| FR-09 | Відхилення кількості меншої за 1 | UC-04 | UC04-S03 | [SC-03](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-03-invalid-quantity.md) |
| FR-10 | Перевірка складського залишку | UC-04 | UC04-S01, UC04-S02 | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md), [SC-02](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-02-insufficient-stock.md) |
| FR-11 | Відхилення замовлення за нестачі примірників | UC-04 | UC04-S02 | [SC-02](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-02-insufficient-stock.md) |
| FR-12 | Перевірка обов'язкових контактних даних | UC-04 | UC04-S04 | [SC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-04-missing-contacts.md) |
| FR-13 | Створення ORDER та ORDER_ITEM | UC-04 | UC04-S01 | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) |
| FR-14 | Фіксація ціни та обчислення суми позиції | UC-04 | UC04-S01 | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) |
| FR-15 | Підтвердження успішного оформлення | UC-04 | UC04-S01 | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) |

## Покриття Gherkin-сценаріїв UC-04

- UC04-S01 — успішне оформлення замовлення: FR-07, FR-10, FR-13, FR-14, FR-15 → [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md). Діаграма показує перевірку даних і залишків, створення замовлення, фіксацію ціни, обчислення вартості позицій та підтвердження покупцеві. Також враховано FR-08 щодо заборони порожнього замовлення.
- UC04-S02 — недостатньо примірників: FR-10, FR-11 → [SC-02](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-02-insufficient-stock.md). Діаграма показує перевірку залишку, відхилення замовлення, повідомлення про доступну кількість та можливість змінити її.
- UC04-S03 — недопустима кількість: FR-09 → [SC-03](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-03-invalid-quantity.md). Діаграма показує перевірку кількості примірників і відхилення замовлення, якщо кількість менша за 1.
- UC04-S04 — відсутні обов'язкові контактні дані: FR-12 → [SC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-04-missing-contacts.md). Діаграма показує перевірку контактних даних і відмову в оформленні замовлення, якщо обов'язкові поля не заповнені.

## Узгодженість з ER-моделлю Завдання №1

| Діаграма | Сутності та їхня роль |
|---|---|
| SC-01 | EDITION — перевірка залишку та отримання актуальної ціни; ORDER — створення замовлення; ORDER_ITEM — створення позицій із кількістю та зафіксованою ціною. |
| SC-02 | EDITION — отримання інформації про доступний залишок; ORDER та ORDER_ITEM не створюються. |
| SC-03 | EDITION — вибране покупцем видання; перевірка кількості відбувається без звернення до бази даних і створення замовлення. |
| SC-04 | ORDER та ORDER_ITEM не створюються через відсутність обов'язкових контактних даних; реєстрація USER для оформлення не потрібна. |

## Висновок

Я з допомогою ШІ створила чотири Sequence Diagram, які описують успішне оформлення замовлення та три помилкові сценарії. Діаграми відображають перевірку контактних даних, кількості примірників, складських залишків, створення замовлення та фіксацію ціни. Кожен сценарій пов'язаний із відповідними функціональними вимогами та Gherkin із Завдання №2. Матриця показує зв'язок між вимогами, сценаріями взаємодії та сутностями ER-моделі Завдання №1.
