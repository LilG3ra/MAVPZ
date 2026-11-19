# DEFENSE — Завдання 1: Домен і модель даних (ER)

## 1. Що я просила у ШІ

Я використала штучний інтелект для аналізу джерел, які були надані для завдання. Завдяки цьому я швидше ознайомилася з вимогами дисципліни, але предметну область обирала самостійно.

Для побудови ER-діаграми я звернулася по допомогу до ШІ та обрала Mermaid. Під час роботи постійно уточнювала інформацію в чатах, обговорювала структуру проєкту та розглядала різні варіанти моделювання. Остаточні рішення приймала самостійно на основі власного аналізу.

Для створення діаграми я зібрала основні положення своєї концептуальної моделі, бізнес-правила та межі роботи в один запит до Mermaid AI. Отриману діаграму повторно перевірила за допомогою ChatGPT, виявила невідповідності та скорегувала її через повторний запит до Mermaid. Фінальний варіант моделі затвердила самостійно.

**Усі промпти:**

- [Промпт 01 — Аналіз матеріалів дисципліни](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/01-prompt.md)
- [Промпт 02 — Структура репозиторію](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/02-prompt.md)
- [Промпт 03 — Початковий опис предметної області](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/03-prompt.md)
- [Промпт 04 — Створення ER-діаграми в Mermaid](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/04-prompt.md)
- [Промпт 05 — Уточнення ER-діаграми в Mermaid](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/05-prompt.md)

## 2. Топ-3 розбіжності, які я знайшла та виправила (spec ↔ вихід ШІ)

**1) Неправильний зв'язок між покупцем і замовленням.**

Початкова діаграма використовувала сутність CUSTOMER і вимагала, щоб покупець був зареєстрований для оформлення замовлення. Це суперечило моїй початковій ідеї, оскільки магазин повинен підтримувати покупки без реєстрації.

Я вирішила використовувати назву USER, замінила `customer_id` на `user_id` та зробила зв'язок USER–ORDER необов'язковим з боку замовлення. Тепер система підтримує як зареєстрованих користувачів, так і гостьові покупки.

**Мій слід:**
[початковий промпт](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/04-prompt.md),
[початковий огляд](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/04-review.md),
[запит на виправлення](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/05-prompt.md),
[огляд результату](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/05-review.md),
[специфікація](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/spec.md).

**Виправлення:** [коміт c872ef1](https://github.com/LilG3ra/MAVPZ/commit/c872ef1).

**2) Неправильна кардинальність між виданням і видавництвом.**

У початковій діаграмі зв'язок EDITION–PUBLISHER був 1:1. Це суперечило логіці предметної області, оскільки одне видавництво може випускати багато різних видань.

Я змінила кардинальність на 1:N. Тепер кожне видання належить одному видавництву, а видавництво може бути пов'язане з багатьма виданнями.

**Мій слід:**
[початковий промпт](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/04-prompt.md),
[початковий огляд](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/04-review.md),
[запит на виправлення](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/05-prompt.md),
[специфікація](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/spec.md).

**Виправлення:** [коміт c872ef1](https://github.com/LilG3ra/MAVPZ/commit/c872ef1).

**3) Замовлення могло не містити жодної позиції.**

Початкова кардинальність ORDER–ORDER_ITEM допускала нуль позицій. Це суперечило початковим бізнес-правилам, за якими замовлення повинно містити хоча б один товар.

Я вирішила залишити для першої версії системи правило, що кожне замовлення має щонайменше одну позицію. Відповідну кардинальність уточнила в ER-діаграмі та узгодила з актуальною специфікацією.

**Мій слід:**
[початковий промпт](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/04-prompt.md),
[запит на виправлення](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/05-prompt.md),
[огляд результату](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/ai/05-review.md),
[специфікація](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/spec.md).

**Виправлення:** [коміт c872ef1](https://github.com/LilG3ra/MAVPZ/commit/c872ef1).

**Додаткові коміти, які підтверджують роботу:**

- [8578e72](https://github.com/LilG3ra/MAVPZ/commit/8578e72) — оновлено зображення ER-діаграми.
- [5c59bef](https://github.com/LilG3ra/MAVPZ/commit/5c59bef) — оновлено опис ER-моделі згідно з виправленнями діаграми.
- [3d7de1f](https://github.com/LilG3ra/MAVPZ/commit/3d7de1f) — уточнено специфікацію ER-моделі.
- [b6f97e5](https://github.com/LilG3ra/MAVPZ/commit/b6f97e5) — уточнено запит до Mermaid AI.

## 3. Ключове рішення

Я вирішила спростити модель онлайн-книгарні та залишити лише 8 основних сутностей, щоб не ускладнювати першу лабораторну роботу.

Для кожної книги передбачила одного автора й один основний жанр. Оплату та доставку вирішила не виділяти в окремі сутності, а зберігати їхні дані в ORDER. Складські залишки обліковуються на рівні EDITION.

Це дозволило зробити ER-діаграму зрозумілішою, зберігши основні можливості системи. Недоліком такого рішення є обмежена деталізація, але в майбутньому модель можна буде розширити.

**Обґрунтування рішень:**

- [ADR-01 — Вибір предметної області та структури моделі](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/adr/01-domain-model.md)
- [ADR-02 — Моделювання зв'язків між сутностями](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/adr/02-relationships-modeling.md)
- [ADR-03 — Вибір формату ER-діаграми](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/adr/03-diagram-format.md)

## 4. Перевірка

Для перевірки результату я зіставила вимоги зі [специфікації](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/spec.md) з актуальною [ER-моделлю](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/diagrams/er-model.mmd).

Основну увагу приділила наявності восьми сутностей, правильності зв'язків і кардинальностей, підтримці гостьових замовлень, обов'язковості позицій замовлення та унікальності ISBN.

Для відтворення діаграми використовується [Mermaid Live Editor](https://mermaid.live/). Потрібно вставити код із файлу [er-model.mmd](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/diagrams/er-model.mmd) та порівняти результат із [графічною версією діаграми](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/diagrams/Діаграма.png).

**Результат перевірки:** Після фактичної перевірки зазначити, чи виконані критерії К1–К7 та чи діаграма відобразилася без помилок.

Усі матеріали лабораторної роботи розміщено в директорії [task-1-domain-er](https://github.com/LilG3ra/MAVPZ/tree/main/task-1-domain-er).
