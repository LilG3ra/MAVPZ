# Завдання №3 — Взаємодія (Sequence Diagram)

**Дисципліна:** Компоненти програмної інженерії.  
**Тема проєкту:** Інформаційна система онлайн-магазину друкованих книг.  

## Опис проєкту

Проєкт продовжує Завдання №1 (ER-модель) та Завдання №2 (вимоги, Use Cases і Gherkin) і присвячений моделюванню взаємодій між покупцем, інтерфейсом, сервісами та базою даних. Покупець може переглядати каталог, шукати книги, отримувати інформацію про книги та видання й оформлювати замовлення без обов'язкової реєстрації. Працівник магазину переглядає та опрацьовує замовлення.

## Мета завдання

Побудувати UML Sequence Diagram для сценаріїв використання із Завдання №2, показати послідовність викликів і відповідей між учасниками, activation bars та комбіновані фрагменти `alt` і `loop`. Перевірити відповідність діаграм сценаріям Gherkin, функціональним вимогам і ER-моделі попередніх завдань.

## Обраний сценарій використання

Для деталізації обрано **UC-04 — Оформити замовлення**. Покупець обирає видання та кількість примірників, вводить контактні дані й підтверджує замовлення. Система перевіряє дані та залишки, а за успішного оформлення створює замовлення із зафіксованою ціною.

Для UC-04 підготовлено чотири Sequence Diagram:

| Gherkin-сценарій | Діаграма | Зміст |
|---|---|---|
| UC04-S01 | [SC-01 — Успішне оформлення](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) | Перевірки, створення `ORDER` та `ORDER_ITEM`, розрахунок вартості й підтвердження. |
| UC04-S02 | [SC-02 — Недостатньо примірників](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-02-insufficient-stock.md) | Відхилення замовлення, повідомлення про доступну кількість і можливість її змінити. |
| UC04-S03 | [SC-03 — Недопустима кількість](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-03-invalid-quantity.md) | Відхилення замовлення за кількості меншої за 1. |
| UC04-S04 | [SC-04 — Відсутні контактні дані](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-04-missing-contacts.md) | Перевірка обов'язкових контактів та відмова в оформленні. |

Вихідні файли Mermaid: [SC-01.mmd](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01.mmd), [SC-02.mmd](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-02.mmd), [SC-03.mmd](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-03.mmd) та [SC-04.mmd](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-04.mmd).

## Основні учасники

- Customer — покупець, який обирає видання та оформлює замовлення.
- OrderUI — інтерфейс для введення даних і відображення результатів.
- OrderService — перевіряє дані, координує оформлення та формує підсумок замовлення.
- StockService — перевіряє доступну кількість примірників.
- Database — повертає дані про видання та забезпечує транзакційне збереження замовлення.

У SC-03 і SC-04 перевірка завершується до звернення до складських залишків, тому ці діаграми не містять StockService і Database.

## Основні бізнес-правила

- Замовлення можна оформити без обов'язкової реєстрації.
- Замовлення має містити щонайменше одну позицію.
- Кожна позиція `ORDER_ITEM` пов'язана з конкретним `EDITION`.
- Кількість примірників має бути більшою за нуль і не перевищувати доступний залишок.
- Ціна фіксується під час оформлення замовлення, а вартість позиції обчислюється за кількістю та зафіксованою ціною.
- За некоректних даних або недостатнього залишку замовлення не створюється. Успішне створення відбувається в межах транзакції.

## Структура проєкту

```text
task-3-sequence-diagram/
├── adr/                 # Прийняті рішення та їх обґрунтування
├── ai/                  # Запити до ШІ та огляди результатів
├── diagrams/            # Sequence Diagram у форматах Markdown і Mermaid
├── spec.md              # Специфікація завдання
├── traceability.md      # Матриця трасування
├── CHECKLIST.md         # Перевірка готовності
├── DEFENSE.md           # Матеріали для захисту
└── README.md            # Опис проєкту
```

## Документація

- [`spec.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/spec.md) — специфікація завдання та критерії прийняття.
- [`diagrams/SC-01-success.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) — опис і перегляд успішного оформлення замовлення.
- [`diagrams/SC-02-insufficient-stock.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-02-insufficient-stock.md) — опис і перегляд сценарію недостатнього залишку.
- [`diagrams/SC-03-invalid-quantity.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-03-invalid-quantity.md) — опис і перегляд сценарію недопустимої кількості.
- [`diagrams/SC-04-missing-contacts.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-04-missing-contacts.md) — опис і перегляд сценарію відсутніх контактних даних.
- [`diagrams/SC-01.mmd`](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01.mmd) — вихідний код Mermaid для успішного оформлення.
- [`diagrams/SC-02.mmd`](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-02.mmd) — вихідний код Mermaid для перевірки залишків.
- [`diagrams/SC-03.mmd`](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-03.mmd) — вихідний код Mermaid для перевірки кількості.
- [`diagrams/SC-04.mmd`](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-04.mmd) — вихідний код Mermaid для перевірки контактних даних.
- [`traceability.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/traceability.md) — матриця трасування вимог, Gherkin і Sequence Diagram.
- [`adr/`](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/adr) — обґрунтування трьох прийнятих рішень.
- [`ai/`](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai) — запити до ШІ, огляди та історія перевірок.
- [`CHECKLIST.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/CHECKLIST.md) — чекліст готовності завдання.
- [`DEFENSE.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/DEFENSE.md) — матеріали для підсумкового захисту.

## Джерела вимог

- [Use Cases із Завдання №2](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/use-cases.md)
- [Функціональні вимоги EARS](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/requirements/functional.md)
- [Gherkin-сценарії UC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/scenarios/UC-04-order-scenario.md)
- ER-модель Завдання №1 — основа для сутностей `EDITION`, `ORDER` та `ORDER_ITEM`.

Документи попередніх завдань не копіюються до Завдання №3. Для зв'язку між ними використовується [матриця трасування](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/traceability.md).

## Перегляд діаграм

Діаграми створено за допомогою Mermaid. У Markdown-файлах на GitHub вони відображаються безпосередньо з блоків `mermaid`, тому окремі зображення не потрібні. Для редагування можна використати [Mermaid Live](https://mermaid.live/).

## Межі роботи

Завдання охоплює моделювання взаємодій під час оформлення замовлення. Реалізація вебзастосунку, бази даних, онлайн-оплати та інтеграції з поштовими службами не входить до роботи.


