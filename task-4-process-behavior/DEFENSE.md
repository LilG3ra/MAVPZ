# Завдання №4 — Процес / поведінка (Activity Diagram)

## 1. Що я просила у ШІ

В завданні №4 я використала ChatGPT та Mermaid AI. З самого початку просила в ШІ проаналізувати вимоги завдання №4, пояснити всі абревіатури та порівняти п'ять запропонованих варіантів реалізації діаграм.  Після порівняння я обрала Activity Diagram у Mermaid Flowchart, тому що в мене є практика та опит виконання з минулих завдань, а ще GitHub може автоматично перетворювати код Mermaid в діаграму, це дуже зручно. За основу я взяла ER-модель із Завдання №1, функціональні вимоги та Gherkin із Завдання №2 і чотири Sequence Diagram із Завдання №3. На відміну від попереднього завдання, цього разу я вирішила об'єднати всі чотири сценарії із UC-04 в одну діаграму. Ще, за допомогою ШІ також підготувала чеклист, матрицю трасування, три ADR та README.md. Підготувала мається на увазі прискорила створення, це означає, що я відправила промпт шаблона, скидувала деякі завдання з попередніх робіт, та казала ШІ створити такий самий шаблон, але казала, який текст замінити. Текст я надавала сама, а все, що було згенеровано додатково без мого відома я перевіряла, та вирішила оставляти чи ні. Для перегляду діаграми використала [Mermaid Live](https://mermaid.live/).

**Записи взаємодії з ШІ та огляди:**

- [Взаємодія 01 - Аналіз матеріалів та вимог Завдання №4](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/01-prompt.md) та [Огляд 01](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/01-review.md).
- [Взаємодія 02 - Порівняння нотацій та вибір типу діаграми](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/02-prompt.md) та [Огляд 02](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/02-review.md).
- [Взаємодія 03 - Визначення структури завдання](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/03-prompt.md) та [Огляд 03](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/03-review.md).
- [Взаємодія 04 - Створення Activity Diagram та виправлення її відображення](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/04-prompt.md) та [Огляд 04](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/04-review.md).
- [Взаємодія 05 - Створення матриці трасування](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/05-prompt.md) та [Огляд 05](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/05-review.md).
- [Взаємодія 06 - Створення ADR та обґрунтування прийнятих рішень](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/06-prompt.md) та [Огляд 06](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/06-review.md).
- [Взаємодія 07 - Створення README.md та приведення до єдиного шаблону](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/07-prompt.md) та [Огляд 07](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/ai/07-review.md).

Усі запити до ШІ, огляди отриманих результатів, мої зауваження та внесені виправлення зберігаються в папці [ai/](https://github.com/LilG3ra/MAVPZ/tree/main/task-4-process-behavior/ai/).

## 2. Топ-3 розбіжності, які я знайшла та виправила (spec ↔ вихід ШІ)

## 3. Ключове рішення

До завдання №4 я обрала з запропонованих варіантів Activity Diagram у Mermaid Flowchart, тому що вона може об'єднати всі сценарії, в моєму випадку, це - 4 в одну діаграму і показати послідовні дії, розгалудження, паралельні процеси і обробку помилок. Для паралельної перевірки використала Fork/Join, а саме для перевірки наявності позицій та допустимих кількостей всередині validateItems(). Спочатку перевіряються контактні дані, а потім залишки, вже після завершення валідації. Також я обрала спільний механізм обробки помилок із можливістю повторного оформлення або припинення процесу.Якщо станеться помилка активної транзакції, то передбачено rollback(), а в разі недостатньої кількості примірників отримується актуальний залишок.

Як і в Завданні №3, я не дублювала матеріали попередніх завдань, а використала посилання та [матрицю трасування](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/traceability.md).

**Обґрунтування рішень:**

- [ADR-01 — Використання Mermaid Flowchart для Activity Diagram](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/adr/01-activity-notation.md).
- [ADR-02 — Використання паралельних перевірок Fork/Join](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/adr/02-parallel-validation.md).
- [ADR-03 — Обробка помилок, rollback та повторне оформлення замовлення](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/adr/03-error-handling.md).
  
## 4. Перевірка

Під час перевірки я порівняла  Activity Diagram зі [специфікацією](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/spec.md), [функціональними вимогами](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/requirements/functional.md), [Gherkin-сценаріями UC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/scenarios/UC-04-order-scenario.md) та [Sequence Diagram Завдання №3](https://github.com/LilG3ra/MAVPZ/tree/main/task-3-sequence-diagram/diagrams). В тому числі переглянула учасників процесу, порядок перевірок, розгалуження if/else, Fork/Join, Send Signal, Accept Event, транзакційне оформлення замовлення та можливість повторної спроби. В матриці трасування перевірила відображення зв'язків з дев'ятьма функціональними вимогами та дев'ятьма Gherkin-сценаріями, як результат перевірки: все виконано коректно. Також я перевірила повторно рендер, оскільки виникли проблеми з відображенням діаграми, тому на неї я змістила більше фокусу, ніж на інші моменти. Реальне тестування застосунку не проводила, оскільки завдання передбачає моделювання поведінки системи, а не її програмну реалізацію.

Усі матеріали третього завдання розміщуються в директорії [task-4-process-behavior](https://github.com/LilG3ra/MAVPZ/tree/main/task-4-process-behavior).
