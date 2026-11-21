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



**3) Замовлення могло не містити жодної позиції.**



**Додаткові коміти, які підтверджують роботу:**



## 3. Ключове рішення



**Обґрунтування рішень:**

- [ADR-01 — Оформлення замовлення без обов'язкової реєстрації](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/adr/01-guest-checkout.md)
- [ADR-02 — Перевірка наявності примірників під час замовлення](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/adr/02-stock-validation.md)
- [ADR-03 — Вибір зв'язків на Use Case-діаграмі](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/adr/03-use-case-relations.md)

## 4. Перевірка




