# Завдання №4 — Процес / поведінка (Activity Diagram)

**Дисципліна:** Компоненти програмної інженерії.  
**Тема проєкту:** Інформаційна система онлайн-магазину друкованих книг.  

## Опис проєкту

Проєкт продовжує Завдання №1 (ER-модель), Завдання №2 (вимоги, Use Cases і Gherkin) та Завдання №3 (Sequence Diagram) і присвячений моделюванню процесу та поведінки системи під час оформлення замовлення в онлайн-магазині друкованих книг. Покупець може переглядати каталог, шукати книги, отримувати інформацію про книги та видання й оформлювати замовлення без обов'язкової реєстрації. Працівник магазину переглядає та опрацьовує замовлення.

## Мета завдання

Деталізувати UC-04 із Завдання №2 за допомогою Activity Diagram, показати послідовність дій, умови переходів, розгалуження if/else, паралельні процеси Fork/Join, цикли, надсилання та отримання повідомлень Send Signal і Accept Event. Перевірити відповідність діаграми сценаріям Gherkin, функціональним вимогам, ER-моделі та Sequence Diagram попередніх завдань.

## Обраний сценарій використання

Для деталізації обрано **UC-04 — Оформити замовлення**. Покупець обирає видання та кількість примірників, вводить контактні дані й підтверджує замовлення. Система перевіряє дані та залишки, а за успішного оформлення створює замовлення із зафіксованою ціною. На одній Activity Diagram об'єднано чотири сценарії з попередніх завдань:

| Gherkin-сценарій | Sequence Diagram | Зміст |
|---|---|---|
| UC04-S01 | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) | Перевірки, транзакційне створення ORDER та ORDER_ITEM, розрахунок вартості й підтвердження. |
| UC04-S02 | [SC-02](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-02-insufficient-stock.md) | Відхилення замовлення, повідомлення про доступну кількість і можливість її змінити. |
| UC04-S03 | [SC-03](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-03-invalid-quantity.md) | Відхилення замовлення за кількості меншої за 1. |
| UC04-S04 | [SC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-04-missing-contacts.md) | Перевірка обов'язкових контактів та відмова в оформленні. |

[Activity Diagram UC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/diagrams/UC-04-activity.md)

Вихідний файл Mermaid: [UC-04-activity.mmd](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/diagrams/UC-04-activity.mmd).

## Основні учасники

- Customer — покупець, який обирає видання та оформлює замовлення.
- OrderUI — інтерфейс для введення даних і відображення результатів.
- OrderService — перевіряє дані, координує оформлення та формує підсумок замовлення.
- StockService — перевіряє доступну кількість примірників.
- Database — повертає дані про видання та забезпечує транзакційне збереження замовлення.

Перевірка контактних даних виконується першою. Після цього паралельно перевіряються наявність позицій та допустимість їхньої кількості. StockService і Database залучаються лише після успішного завершення валідації.

## Основні бізнес-правила

- Замовлення можна оформити без обов'язкової реєстрації.
- Замовлення має містити щонайменше одну позицію.
- Кожна позиція `ORDER_ITEM` пов'язана з конкретним `EDITION`.
- Кількість примірників має бути не меншою за 1 і не перевищувати доступний залишок.
- Однакові видання групуються, а їхня кількість підсумовується перед перевіркою залишків.
- Перевірка наявності позицій та допустимості кількості виконується паралельно через Fork/Join.
- Ціна фіксується під час оформлення замовлення, а вартість позиції обчислюється за формулою `quantity * priceSnapshot`.
- Створення замовлення, його позицій та оновлення залишків виконуються в межах однієї транзакції.
- У разі помилки активної транзакції виконується `rollback()` без збереження часткових змін.
- Якщо під час транзакції виявлено недостатній залишок, після `rollback()` покупцеві повідомляється актуальна доступна кількість примірників.
- Після отримання повідомлення про помилку покупець може виправити дані, повторити спробу або припинити оформлення.

## Структура проєкту

```text
task-4-process-behavior/
├── adr/                 # Прийняті рішення та їх обґрунтування
├── ai/                  # Запити до ШІ та огляди результатів
├── diagrams/            # Activity Diagram у форматах Markdown і Mermaid
├── spec.md              # Специфікація завдання
├── traceability.md      # Матриця трасування
├── CHECKLIST.md         # Перевірка готовності
├── DEFENSE.md           # Матеріали для захисту
└── README.md            # Опис проєкту
```

## Документація

- [`spec.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/spec.md) — специфікація завдання та критерії прийняття.
- [`diagrams/UC-04-activity.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/diagrams/UC-04-activity.md) — опис і графічне представлення процесу оформлення замовлення.
- [`diagrams/UC-04-activity.mmd`](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/diagrams/UC-04-activity.mmd) — вихідний код Mermaid для Activity Diagram.
- [`traceability.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/traceability.md) — матриця трасування вимог, Gherkin, Sequence Diagram та Activity Diagram.
- [`adr/`](https://github.com/LilG3ra/MAVPZ/tree/main/task-4-process-behavior/adr) — обґрунтування трьох прийнятих рішень щодо вибору нотації, паралельних перевірок та обробки помилок.
- [`ai/`](https://github.com/LilG3ra/MAVPZ/tree/main/task-4-process-behavior/ai) — запити до ШІ, огляди та історія перевірок.
- [`CHECKLIST.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/CHECKLIST.md) — чеклист готовності завдання.
- [`DEFENSE.md`](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/DEFENSE.md) — матеріали для підсумкового захисту (у підготовці).

## Джерела вимог

- [Use Cases із Завдання №2](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/use-cases.md)
- [Функціональні вимоги EARS](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/requirements/functional.md)
- [Gherkin-сценарії UC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/scenarios/UC-04-order-scenario.md)
- [ER-модель Завдання №1](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/diagrams/er-model.md) — основа для сутностей `EDITION`, `ORDER` та `ORDER_ITEM`.
- [Sequence Diagram Завдання №3](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/diagrams) — основа для визначення учасників, послідовності операцій та повідомлень.
- [Матриця трасування Завдання №3](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/traceability.md)

Документи попередніх завдань не копіюються до Завдання №4. Для зв'язку між ними використовується [матриця трасування](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/traceability.md).

## Перегляд діаграми

Activity Diagram створено за допомогою Mermaid Flowchart. У Markdown-файлі на GitHub діаграма відображається безпосередньо з блоку `mermaid`, тому окреме зображення не потрібне. Для редагування можна використати [Mermaid Live](https://mermaid.live/). Для покращення читабельності на початок Mermaid-коду додано конфігурацію графічного рендерингу, яка визначає спосіб відображення тексту, ширину перенесення, відстані між блоками та внутрішні відступи.

## Межі роботи

Завдання охоплює деталізацію процесу та поведінки системи під час оформлення замовлення UC-04. Реалізація вебзастосунку, бази даних, онлайн-оплати, доставки книг та обов'язкової реєстрації не входить до роботи. Для моделювання використовується одна нотація — Activity Diagram у Mermaid Flowchart. BPMN та машина станів не реалізуються. Матеріали попередніх завдань залишаються незмінними.
