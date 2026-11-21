# DEFENSE — Завдання 2: Вимоги та Use Cases (UC + Gherkin + EARS + NFR)

## 1. Що я просила у ШІ

Як і в завданні №1, я використала ШІ для аналізу джерел, які були надані для завдання. За основу структури проекту завдання №2 я взяла з завдання №1, звідти я швидко перенесла основну частину логіки проекту. Перша робота дала мені ER-модель, ідею доменп онлайн-магазина друрованих книг та предмену область. Пльім я підготувала п'ять основних Use Cases для працівника та покупця магазину, сценарії Gherkin для оформлення замовлення, функціональні вимоги EARS та нефункціональні вимоги NFR. 

Для створення UC-діаграми я використала Mermaid Live. Спочатку після запиту я отримала діаграму із зайвими зв'язками між сценаріями. Після того як я проаналізувала помилки - відправила другий запит в ШІ, щоб виправити ці зв'язки та залишити необхідні.

Також я зверталася до ChatGPT, щоб допоміг оформити вимоги і створити матрицю трасування в GitHub, однак я незнала як робити таблиці, тому було зроблено додатковий запит, направлений на створення таблиці, а саме, щоб ШІ пояснив мені, як її робити. У результаті було підготововлено 18 фунціональних вимог, 7 нефункціональних вимог та таблицю, що пов'язує FR із UC і Gherkin.

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

**1) Непотрібний зв'язок між переглядом каталогу та пошуком книги.**

У першому варіанті UC-діаграми Mermaid додав стрілку між UC-01 "Переглянути каталог книг" та UC-02 "Знайти книгу". Це не відповідало моїй специфікації, оскільки перегляд каталогу та пошук книги є окремими можливостями покупця. Тому, вирішила прибрати цей зв'язок, щоб діаграма не показувала зайву залежність між сценаріями. Покупець повинен мати можливість як переглядати каталог, так і самостійно шукати книги.

**Мій слід:**

- [Промпт 05 — Створення Use Case-діаграми](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/05-prompt.md).
- [Огляд 05 — Аналіз Use Case-діаграми](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/05-review.md).
- [Специфікація](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/spec.md).
- [Актуальна Use Case-діаграма](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/use-cases.md).

**Коміти роботи над виправленнями:**
- [488ca86 — Добавлено експортовану діаграму UC з Mermaid](https://github.com/LilG3ra/MAVPZ/commit/488ca86).
- [0540b2c — Створено UC.md до діаграми](https://github.com/LilG3ra/MAVPZ/commit/0540b2c).
- [d98b935 — Замінено діаграму UC на актуальну](https://github.com/LilG3ra/MAVPZ/commit/d98b935).
- [b8e0d5c — Виправлено діаграму](https://github.com/LilG3ra/MAVPZ/commit/b8e0d5c).
- [6155c31 — Оновлено код діаграми](https://github.com/LilG3ra/MAVPZ/commit/6155c31).
- [ec84b2d — update: Видалено діаграму для подалі коректного завантаження](https://github.com/LilG3ra/MAVPZ/commit/ec84b2d).
- [f7c0281 — fix: Повторно завантажено діаграму](https://github.com/LilG3ra/MAVPZ/commit/f7c0281).

**2) Неправильний зв'язок між пошуком книги та переглядом інформації.**

У початковій діаграмі UC-02 "Знайти книгу" був з'єднаний стрілкою з UC-03 "Переглянути інформацію про книгу та видання". Через це могло скластися враження, що перегляд інформації обов'язково починається з пошуку. Але покупець може відкрити сторінку книги й безпосередньо з каталогу. Тому я вирішила залишити UC-02 та UC-03 окремими сценаріями й прибрати зайву стрілку між ними.

**Мій слід:**

- [Промпт 05 — Створення Use Case-діаграми](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/05-prompt.md).
- [Огляд 05 — Аналіз Use Case-діаграми](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/05-review.md).
- [Опис Use Cases](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/ai/05-review.md).
- [Актуальна Use Case-діаграма](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/use-cases.md).

**Коміти роботи над виправленнями:**

- [b8e0d5c — Виправлено діаграму](https://github.com/LilG3ra/MAVPZ/commit/b8e0d5c).
- [d98b935 — Замінено діаграму UC на актуальну](https://github.com/LilG3ra/MAVPZ/commit/d98b935).
- [f7c0281 — fix: Повторно завантажено діаграму](https://github.com/LilG3ra/MAVPZ/commit/f7c0281).

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

## 3. Ключове рішення

**Обґрунтування рішень:**

- [ADR-01 — Оформлення замовлення без обов'язкової реєстрації](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/adr/01-guest-checkout.md)
- [ADR-02 — Перевірка наявності примірників під час замовлення](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/adr/02-stock-validation.md)
- [ADR-03 — Вибір зв'язків на Use Case-діаграмі](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/adr/03-use-case-relations.md)

## 4. Перевірка
