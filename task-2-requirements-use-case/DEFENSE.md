# DEFENSE — Завдання 2: Вимоги та Use Cases (UC + Gherkin + EARS + NFR)

## 1. Що я просила у ШІ

Як і в першому завданні, я використала ШІ для аналізу матеріалів. За основу взяла свою ER-модель онлайн-магазину друкованих книг та структуру попереднього проєкту. Потім підготувала п'ять Use Cases, сценарії Gherkin, функціональні вимоги EARS та NFR.

Для створення UC-діаграми використала Mermaid Live. У першій версії були зайві зв'язки, тому після аналізу помилок я уточнила запит до ШІ та виправила діаграму.

Також зверталася до ChatGPT по допомогу з оформленням вимог і матриці трасування. Окремо попросила пояснити, як створювати таблиці в GitHub. У результаті підготувала 18 функціональних вимог, 7 NFR та матрицю трасування.

**Усі промпти:**

- [Промпт 01 — Аналіз матеріалів для завдання 2 (Вимоги та Use Cases)](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/01-prompt.md)
- [Промпт 02 — Створення Gherkin-сценаріїв для UC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/02-prompt.md)
- [Промпт 03 — Аналіз Use Cases онлайн-книжкового магазину](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/03-prompt.md)
- [Промпт 04 — Створення структури Завдання №2](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/04-prompt.md)
- [Промпт 05 — Побудова Use Case-діаграми в Mermaid](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/05-prompt.md)
- [Промпт 06 — Перевірка нефункціональних вимог NFR](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/06-prompt.md)
- [Промпт 07 — Створення таблиці в GitHub](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/07-prompt.md)
- [Промпт 08 — Створення матриці трасування вимог](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/08-prompt.md)
- [Промпт 09 — Підготовка трьох ADR](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/09-prompt.md)


## 2. Топ-3 розбіжності, які я знайшла та виправила (spec ↔ вихід ШІ)

**1) Зайвий зв'язок між переглядом каталогу та пошуком книги.**

У першій UC-діаграмі Mermaid додав стрілку між UC-01 та UC-02, хоча це окремі дії покупця. Я вирішила прибрати цей зв'язок, щоб діаграма відповідала моїй специфікації.

**Мій слід:** [Промпт 05](ai/05-prompt.md), [Огляд 05](ai/05-review.md), [Специфікація](spec.md).

**Коміти:** [b8e0d5c](https://github.com/LilG3ra/MAVPZ/commit/b8e0d5c), [6155c31](https://github.com/LilG3ra/MAVPZ/commit/6155c31).

**2) Неправильний зв'язок між пошуком книги та переглядом інформації.**

Початкова діаграма показувала залежність UC-03 від UC-02, хоча покупець може відкрити інформацію про книгу безпосередньо з каталогу. Тому я прибрала зайву стрілку й залишила ці сценарії окремими.

**Мій слід:** [Промпт 05](ai/05-prompt.md), [Огляд 05](ai/05-review.md), [Use Cases](use-cases.md).

**Коміт:** [d98b935](https://github.com/LilG3ra/MAVPZ/commit/d98b935).

**3) Зайвий зв'язок між оформленням та опрацюванням замовлення.**

У першій діаграмі UC-04 та UC-05 були з'єднані стрілкою, хоча ці сценарії виконують різні актори. Я прибрала цей зв'язок і залишила тільки `include` між оформленням замовлення та обов'язковою перевіркою залишків.

**Мій слід:** [Промпт 05](ai/05-prompt.md), [Огляд 05](ai/05-review.md), [ADR-03](adr/03-use-case-relations.md).

**Коміти:** [d98b935](https://github.com/LilG3ra/MAVPZ/commit/d98b935), [f7c0281](https://github.com/LilG3ra/MAVPZ/commit/f7c0281).


**3) Зайвий зв'язок між оформленням та опрацюванням замовлення.**

На початковій діаграмі UC-04 "Оформити замовлення" був з'єднаний із UC-05 "Опрацювати замовлення". Це неправильно відображало взаємодію акторів, оскільки покупець оформлює замовлення, а працівник магазину опрацьовує його окремо. Я вирішила прибрати цей зв'язок і залишити тільки необхідні асоціації акторів зі сценаріями. Також на діаграмі залишила один зв'язок `include` між UC-04 та перевіркою наявності примірників, тому що така перевірка обов'язкова під час оформлення замовлення. Завдяки цьому фінальна діаграма стала простішою та краще відповідає бізнес-правилам мого онлайн-магазину.

**Мій слід:**

- [Промпт 05 — Створення Use Case-діаграми](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/05-prompt.md).
- [Огляд 05 — Аналіз Use Case-діаграми](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/05-review.md).
- [Специфікація](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/spec.md).
- [ADR-03 — Вибір зв'язків на Use Case-діаграмі](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/adr/03-use-case-relations.md).

**Коміти роботи над виправленнями:**

- [d98b935 — Замінено діаграму UC на актуальну](https://github.com/LilG3ra/MAVPZ/commit/d98b935).
- [f7c0281 — Повторно завантажено діаграму](https://github.com/LilG3ra/MAVPZ/commit/f7c0281).

**Додаткові коміти, які підтверджують роботу над діаграмою:**

- [2fa09bd — Додано код із Mermaid](https://github.com/LilG3ra/MAVPZ/commit/2fa09bd).
- [0540b2c — Створено UC.md до діаграми](https://github.com/LilG3ra/MAVPZ/commit/0540b2c).
- [b8e0d5c — Виправлено діаграму](https://github.com/LilG3ra/MAVPZ/commit/b8e0d5c).
- [ec84b2d — update: Видалено діаграму для подалі коректного завантаження](https://github.com/LilG3ra/MAVPZ/commit/ec84b2d).

## 3. Ключове рішення

Під час виконання завдання я залишила п'ять Use Cases та двох акторів. Основну увагу приділила оформленню замовлення. Вирішила залишити можливість покупки без реєстрації та обов'язкову перевірку залишків. Також прибрала зайві стрілки на UC-діаграмі, залишивши необхідні зв'язки та `include` для перевірки примірників. Детальніше ці рішення описані в ADR-01, ADR-02 та ADR-03.

**Обґрунтування рішень:**

- [ADR-01 — Оформлення замовлення без обов'язкової реєстрації](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/adr/01-guest-checkout.md)
- [ADR-02 — Перевірка наявності примірників під час замовлення](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/adr/02-stock-validation.md)
- [ADR-03 — Вибір зв'язків на Use Case-діаграмі](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/adr/03-use-case-relations.md)

## 4. Перевірка

Для перевірки завдання я зіставила вимоги зі [специфікації](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/spec.md) з Use Cases, діаграмою та Gherkin-сценаріями. Перевірила зв'язки акторів, прибрала зайві залежності та залишила обов'язкову перевірку залишків для UC-04. Також підготувала чотири Gherkin-сценарії, перевірила 18 функціональних вимог EARS і 7 NFR. Для зв'язку між вимогами та сценаріями створила [матрицю трасування](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/traceability.md). Діаграму виправила через [Mermaid Live](https://mermaid.live/) та оновила в GitHub.

**Результат перевірки:** я підготовила основні, а виявлені зайві зв'язки на Use Case-діаграмі виправила. Функціональні вимоги, Gherkin-сценарії та матриця трасування узгоджені між собою на рівні описаної системи раніше. Реальне тестування програмного застосунку не проводилося, оскільки завдання передбачає створення документації та моделювання вимог, тому я не виконувала лишньої роботи.

Усі матеріали другого завдання розміщено в директорії [task-2-requirements-use-case](https://github.com/LilG3ra/MAVPZ/tree/main/task-2-requirements-use-case).
