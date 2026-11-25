# DEFENSE — Завдання 3: Взаємодія (Sequence Diagram)

## 1. Що я просила у ШІ

Як і в завданні №1 та №2, я використала ШІ ChatGPT та Mermaid. В основному я їх використовувала для генерації діаграм. За основу я взяла ER-модель із завдання №1 та use case (UC). Функціональні вимони та Gherkin я взала із завдання №2. Спочатку я за допомогою ШІ проаналізувала джерела, які йому надала, потім запитала за структуру проєкта, я не захотіла створювати зайві дублікати файли, та запитала в чата GPT як йому ідея просто створити посилання на вже існуючі файли. Ідея з посиланням виявилась дуже зручною та не потрібно було створювати дуже багато непотрібних дублікатів. Для перевірки діаграм після генерування я використала [Mermaid Live](https://mermaid.live/). 

**Записи взаємодії з ШІ та огляди:**

- [Взаємодія 03 — Створення чотирьох Sequence Diagram](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/03-prompt.md) та [Огляд 03](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/03-review.md).
- [Взаємодія 04 — Перевірка та виправлення діаграм](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/04-prompt.md) та [Огляд 04](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/04-review.md).
- [Взаємодія 05 — Фінальні виправлення SC-01 та SC-02](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/05-prompt.md) та [Огляд 05](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/05-review.md).

Запити про роботу з ШІ зберігаються в папці [ai/](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/).

## 2. Топ-3 розбіжності, які я знайшла та виправила (spec ↔ вихід ШІ)

**1) Недостатньо точно враховувалися однакові видання в SC-01.**

В першій версії SC-01 перевірка залишків не показувала групування позицій за виданням. Якщо покупець кілька разів додає одне видання, потрібно врахувати загальну замовлену кількість. Я додала за допомогою ШІ aggregateItemsByEdition(items[]) і уточнила перевірку сумарної кількості. Також доповнила створення ORDER_ITEM параметром orderId, щоб показати зв'язок позиції із замовленням. Початкова модель вже містила транзакцію та rollback(), тому я не створювала цей механізм заново, а просто уточнила його опис.

**Мій слід:** [Взаємодія 04](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/04.md), [Огляд 04](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/review-04.md), [SC-01](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/diagrams/SC-01-success.md).

**Коміти:** [5015870 — уточнення коду відповідно до Gherkin](https://github.com/LilG3ra/MAVPZ/commit/5015870), [5015870 — коригування коду відповідно до Gherkin](https://github.com/LilG3ra/MAVPZ/commit/5015870).

**2) У SC-01 не було явно показано обчислення вартості позиції.**

За FR-14 та UC04-S01 система повинна зафіксувати ціну примірника й показати суму позиції. Спочатку в діаграмі був priceSnapshot, але окремого розрахунку не вистачало. Я доповнила SC-01 операцією calculateItemTotal(quantity, priceSnapshot) і формулою itemTotal = quantity * priceSnapshot. Формування підсумку замовлення перенесла до OrderService, а Database передає збережені позиції через orderCreated(orderId, savedItems[]).

**Мій слід:** [Взаємодія 05](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/05.md), [Огляд 05](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/review-05.md), [SC-01](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/diagrams/SC-01-success.md), [FR-14 у матриці](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/traceability.md).

**Коміти:** [4a15609 — оновлення коду SC-01](https://github.com/LilG3ra/MAVPZ/commit/4a15609).

**3) У SC-02 повідомлення про нестачу примірників було занадто загальним.**

У Gherkin UC04-S02 зазначено, що покупець має побачити доступну кількість примірників і мати можливість змінити замовлену кількість. У початковій SC-02 було лише загальне повідомлення про недостатній залишок. Я додала передавання available через orderRejected(outOfStock, available), оновила showOutOfStockError(available) та додала showQuantityChangeOption(). Логіка відхилення замовлення без створення ORDER і ORDER_ITEM залишилася без змін.

**Мій слід:** [Взаємодія 05](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/05.md), [Огляд 05](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/review-05.md), [SC-02](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/diagrams/SC-02-insufficient-stock.md), [FR-11 у матриці](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/traceability.md).

**Коміти:** [1d06ae2 — виправлення SC-02 відповідно до Gherkin](https://github.com/LilG3ra/MAVPZ/commit/1d06ae2), [f391b4b — оновлення коду SC-02](https://github.com/LilG3ra/MAVPZ/commit/f391b4b).

## 3. Ключове рішення

Для завдання №3 я взяла UC-04 та створила чотири окремі Sequence Diagram замість однієї великої. Діаграми побудувала в Mermaid за допомогою ШІ, це зручно, тому що потім я можу їх переглянути в Mermaid Live, внести код в Markdown GitHub, де GitHub сам компілює код в діаграму, а зміни я можу відстежити через комміти.

Я вирішила не копіювати Use Cases, вимоги та Gherkin із Завдання №2, а також інші файли. Замість цього я зробила набагато бистріше: залишила посилання на попередні матеріали та створила [матрицю трасування](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/traceability.md). Для SC-01 я зберегла транзакційне оформлення замовлення з повторною перевіркою залишків, фіксацією ціни та rollback() у разі помилки.

**Обґрунтування рішень:**

- [ADR-01 — Використання Mermaid для Sequence Diagram](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/adr/01-mermaid-sequence-diagrams.md).
- [ADR-02 — Використання посилань замість дублювання документів](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/adr/02-links-instead-of-duplicates.md).
- [ADR-03 — Транзакційне оформлення замовлення](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/adr/03-transactional-order-processing.md).

## 4. Перевірка

Під час перевірки я порівняла чотири діаграми з [специфікацією](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/spec.md), [функціональними вимогами Завдання №2](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/requirements/functional.md) та [Gherkin-сценаріями UC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/scenarios/UC-04-order-scenario.md). Переглянула учасників, порядок повідомлень, return-повідомлення, activation bars, фрагменти alt і loop та обробку помилок. Виявлені розбіжності в SC-01 та SC-02 виправила і зберегла зміни в GitHub. SC-03 та SC-04 залишила без додаткових змін, оскільки основна логіка відхилення замовлення в них показана правильно. Реальне тестування застосунку не проводила, оскільки завдання передбачає створення діаграм, а не розробку системи.

Усі матеріали третього завдання розміщуються в директорії [task-3-sequence-diagram](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram).

