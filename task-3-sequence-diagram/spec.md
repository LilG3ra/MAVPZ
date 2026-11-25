# Специфікація — Завдання №3: Взаємодія (Sequence Diagram)

## 1. Мета

Потрібно побудувати чотирі діаграми послідовності для UC-04 (Оформити замовлення), яке в [завданні №2](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/diagrams/UC.md). Також, необхідно показати послідовність повідомлень, які відбуваються між покупцем, інтерфейсом, сервісами і базою даних. Це все має бути включно з відповідями, activation bars та комбінованими фрагментами alt; loop. Треба перевірити узгодженість з [Gherkin](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/scenarios/UC-04-order-scenario.md), [use cases](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/diagrams/UC.md), [ER-моделлю](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/diagrams/er-model.md), які я зробила в попередніх завданнях.

## 2. Опис предметної області

Мій онлайн-магазин книжок продає друковані книги. Покупець має можливість оформити замовлення без обов'язкової реєстрації Він може обрати конкретне видання EDITION, кількість примірників, але вказати контактні дані. Замовлення (ORDER) містить позиції (ORDER_ITEM). Для кожної з позицій фіксується ціна на момент оформлення заказу.

## 3. Основні сценарії використання

Для моделювання обрано [UC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/diagrams/UC.md) та чотири сценарії з Завдання №2:

[SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) / [UC04-S01](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/scenarios/UC-04-order-scenario.md) — успішне оформлення: перевірка даних і залишків, транзакційне створення замовлення, розрахунок вартості та підтвердження покупцеві.

[SC-02](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-02-insufficient-stock.md) / [UC04-S02](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/scenarios/UC-04-order-scenario.md) — недостатньо примірників: відмова із зазначенням доступної кількості та можливістю змінити замовлену кількість.

[SC-03](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-03-invalid-quantity.md) / [UC04-S03](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/scenarios/UC-04-order-scenario.md) — недопустима кількість: відхилення кількості меншої за 1 без створення замовлення.

[SC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-04-missing-contacts.md) / [UC04-S04](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/scenarios/UC-04-order-scenario.md) — відсутні контактні дані: повідомлення про помилку без створення замовлення.

Серед основних учасників - це: Customer, OrderUI, OrderService, StockService і Database. 

## 4. Зв'язки та бізнес-правила

1. Замовлення можливо зробити без попередньої реєстрації.
2. Замовлення обов'язково повинно містити хоча б одну позицію, яка більше за 0.
3. Кожна позиція (ORDER_ITEM) стосується конкретного EDITION
4. Для правильного замовлення перед створенням залишок видання перевіряється. Якщо видання однакові, то вони враховуються сумарно.
5. Якщо якісь дані неправильні або примірників недостатньо, то ORDER та ORDER_ITEM не створюються.
6. Під час створення відбувається фіксація priceSnapshot, а вартість позиції обчислюється ось так: quantity * priceSnapshot
7. Як замовлення, так і зміна залишків виконуються в межах транзакції. Якщо відбувається помилка, то використовується rollback().

## 5. Критерії прийняття

1. Повинні бути чотири окремі Sequence Diagram у Mermaid (SC-01, SC-02, SC-03, SC-04).

2. На діаграмах повинно бути показано відповідних учасників, виклики, return-повідомлення, activation bars, alt та, де потрібно, loop.

3. SC-01 показує перевірки, транзакцію, створення ORDER і ORDER_ITEM, фіксацію ціни, обчислення суми та підтвердження.

4. SC-02 – SC-04 показують причини відмови та очікувані повідомлення покупцеві без створення замовлення.

5. Діаграми звірено з Gherkin UC04-S01–UC04-S04, вимогами FR-07–FR-15 та сутностями ER-моделі Завдання №1.

6. Підготовлено README.md, traceability.md, CHECKLIST.md, DEFENSE.md, ADR і обов'язково записи запитів та оглядів у ai/. Матеріали попередніх завдань використовуються через посилання, без дублювання.

## 6. Обмеження (Out of Scope)

У цьому завданні розглядається лише взаємодія між покупцем, інтерфейсом, сервісами та базою даних під час оформлення замовлення. Розробка самого вебзастосунку та реалізація бази даних не передбачені. Також не розглядаються онлайн-оплата, доставка книг і обов'язкова реєстрація користувачів. Для побудови Sequence Diagram використовується UC-04 із Завдання №2. Інші сценарії використання окремо не деталізуються. Діаграми повинні відповідати раніше визначеним вимогам і бізнес-правилам.
