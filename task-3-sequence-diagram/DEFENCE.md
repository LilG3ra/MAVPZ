# DEFENSE — Завдання 3: Взаємодія (Sequence Diagram)

## 1. Що я просила у ШІ

Як і в завданні №1 та №2, я використала ШІ ChatGPT та Mermaid. В основному я їх використовувала для генерації діаграм. За основу я взяла ER-модель із завдання №1 та use case (UC). Функціональні вимони та Gherkin я взала із завдання №2. Спочатку я за допомогою ШІ проаналізувала джерела, які йому надала, потім запитала за структуру проєкта, я не захотіла створювати зайві дублікати файли, та запитала в чата GPT як йому ідея просто створити посилання на вже існуючі файли. Ідея з посиланням виявилась дуже зручною та не потрібно було створювати дуже багато непотрібних дублікатів. Для перевірки діаграм після генерування я використала [Mermaid Live](https://mermaid.live/). 

**Записи взаємодії з ШІ та огляди:**

- [Взаємодія 03 — Створення чотирьох Sequence Diagram](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/03-prompt.md) та [Огляд 03](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/03-review.md).
- [Взаємодія 04 — Перевірка та виправлення діаграм](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/04-prompt.md) та [Огляд 04](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/04-review.md).
- [Взаємодія 05 — Фінальні виправлення SC-01 та SC-02](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/05-prompt.md) та [Огляд 05](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/05-review.md).

Запити про роботу з ШІ зберігаються в папці [ai/](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/ai/).

## 2. Топ-3 розбіжності, які я знайшла та виправила (spec ↔ вихід ШІ)



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

