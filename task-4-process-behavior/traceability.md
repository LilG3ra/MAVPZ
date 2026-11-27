# Матриця трасування процесу — онлайн-магазин друкованих книг

## Призначення

Документ пов'язує процес UC-04 (Оформити замовлення), функціональні вимоги, Gherkin-сценарії Завдання №2, Sequence Diagram Завдання №3 та Activity Diagram Завдання №4.

Основою є [ER-модель](https://github.com/LilG3ra/MAVPZ/blob/main/task-1-domain-er/diagrams/er-model.md), [Use Cases](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/diagrams/UC.md), [функціональні вимоги EARS](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/requirements/functional.md), [Gherkin-сценарії](https://github.com/LilG3ra/MAVPZ/blob/main/task-2-requirements-use-case/scenarios/UC-04-order-scenario.md), [матриця трасування Завдання №3](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/traceability.md) та [специфікація Завдання №4](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/spec.md).

Ідентифікатори вузлів наведено відповідно до [вихідного коду Activity Diagram](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/diagrams/UC-04-activity.mmd). Графічне представлення: [Activity Diagram UC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-4-process-behavior/diagrams/UC-04-activity.md).

## Зв'язок функціональних вимог із UC-04, Gherkin, Sequence та Activity Diagram

| Вимога | Короткий зміст | Use Case | Gherkin-сценарій | Sequence Diagram | Вузли Activity Diagram |
|---|---|---|---|---|---|
| FR-07 | Оформлення без реєстрації | UC-04 | Background, UC04-S01–S04 | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) | `START`, `C1`, `UI1`, `C0`, `C2` |
| FR-08 | Заборона порожнього замовлення | UC-04 | Окремий сценарій відсутній | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) | `V1`, `F1`, `V2`, `J1`, `D2` (Ні), `E2`, `REJ1` → `REJ2` → `REJ3` → `MSG4` → `REJ4` |
| FR-09 | Відхилення кількості меншої за 1 | UC-04 | UC04-S03 | [SC-03](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-03-invalid-quantity.md) | `V1`, `F1`, `V3`, `J1`, `D3` (Ні), `E3`, `REJ1` → `REJ2` → `REJ3` → `MSG2` → `REJ4` |
| FR-10 | Перевірка залишків кожного EDITION | UC-04 | UC04-S01, UC04-S02 | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md), [SC-02](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-02-insufficient-stock.md) | `OS3`, `OS4`, `S1`–`S3`, `D4`, `D5`, `DB2`, `D6`–`D8` |
| FR-11 | Повідомлення доступної кількості за нестачі примірників | UC-04 | UC04-S02 | [SC-02](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-02-insufficient-stock.md), [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) (уточнення після rollback) | `D5` (Ні), `DB2`, `D8` (Ні), `RB1`, `OS8`, `OS5`, `OS6`, `D14`, `E4`, `REJ1` → `REJ2` → `REJ3` → `MSG3` → `REJ4`, `D13` |
| FR-12 | Перевірка обов'язкових контактних даних | UC-04 | UC04-S04 | [SC-04](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-04-missing-contacts.md) | `OS2`, `D1` (Ні), `E1`, `REJ1` → `REJ2` → `REJ3` → `MSG1` → `REJ4` |
| FR-13 | Створення одного ORDER та відповідних ORDER_ITEM | UC-04 | UC04-S01 | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) | `DB0`–`DB6`, `D0`, `D6`–`D12`, `RB1`, `RB2` |
| FR-14 | Фіксація ціни та розрахунок вартості позиції | UC-04 | UC04-S01 | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) | `DB2`, `DB4`, `DB6`, `OS7`, `OK1`–`OK4` |
| FR-15 | Підтвердження успішного оформлення | UC-04 | UC04-S01 | [SC-01](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01-success.md) | `D12` (Так), `DB6`, `OS7`, `OK1`–`OK4`, `END` |

## Покриття Gherkin-сценаріїв UC-04

| Сценарій | Відповідний шлях Activity Diagram | Очікуваний результат |
|---|---|---|
| UC04-S01 / SC-01 — успішне оформлення | `D1` (Так) → `F1` / `J1` → `D2`, `D3` (Так) → `D5` (Так) → транзакція → `D12` (Так) → `OK4` | За наявності 5 примірників і замовленні 2 за ціною 300 грн створюється ORDER та ORDER_ITEM; вартість позиції — 600 грн, покупець отримує підтвердження. |
| UC04-S02 / SC-02 — недостатньо примірників | `D5` (Ні) → `E4` → `REJ1` → `REJ2` → `REJ3` → `MSG3` → `REJ4` → `D13` | За замовлення 4 примірників при залишку 2 система повідомляє, що доступно 2; замовлення не створюється, кількість можна змінити. |
| UC04-S03 / SC-03 — недопустима кількість | `D1` (Так) → `F1` / `J1` → `D2` (Так) → `D3` (Ні) → `E3` → `REJ1` → `REJ2` → `REJ3` → `MSG2` → `REJ4` | За кількості 0 система повідомляє, що мінімальна кількість — 1; залишки не перевіряються, замовлення не створюється. Для проходження цього шляху контакти мають бути заповнені. |
| UC04-S04 / SC-04 — відсутні контакти | `D1` (Ні) → `E1` → `REJ1` → `REJ2` → `REJ3` → `MSG1` → `REJ4` → `D13` | Система повідомляє про необхідність заповнення контактів; позиції та залишки не перевіряються, замовлення не створюється. |

FR-08 додатково покривається гілкою `D2` (Ні) → `E2`. Окремого Gherkin-сценарію для порожнього замовлення в Завданні №2 немає.

## Узгодженість повідомлень із Sequence Diagram Завдання №3

| Відправник → отримувач | Повідомлення / операція | Вузли Activity Diagram |
|---|---|---|
| Customer → OrderUI | `selectEditions()`, `enterContactData()`, `submitOrder()` | `C1`, `C0`, `C2`, `UI2` |
| OrderUI → OrderService | `submitOrder(contactData, items[])` | `OS1` |
| OrderService → StockService | `checkStock(editionId, totalQuantity)` | `OS4`, `OS5` |
| StockService → Database | `queryEditionStock(editionId)` | `S1`, `OS5` |
| Database → StockService → OrderService | `available`, `stockCheck()` | `S2`, `S3`, `OS6` |
| OrderService → Database | `createOrderAtomically(contactData, items[])` | `DB0` |
| Database → OrderService | `orderCreated(orderId, savedItems[])`, `orderRejected(outOfStock, insufficientEditionIds)` (уточнення SC-01), `technicalError` | `DB6`, `RB1`, `RB2`, `E5` |
| OrderService → OrderUI | `orderCreated(orderId, summary)`, `orderRejected(reason, available за потреби)` | `OK1`, `OK2`, `REJ1`, `REJ2` |
| OrderUI → Customer | `confirmationMessage()`, `showContactDataError()`, `showQuantityError()`, `showOutOfStockError(available)`, `showQuantityChangeOption()` | `OK3`, `OK4`, `REJ3`, `MSG1`–`MSG5`, `REJ4` |

## Узгодженість з ER-моделлю Завдання №1

| Сутність | Роль у процесі | Вузли Activity Diagram |
|---|---|---|
| EDITION | Вибране видання, групування за editionId, перевірка та оновлення залишків, отримання ціни | `C1`, `OS3`, `OS4`, `S1`–`S3`, `DB2`, `DB4`, `RB1`, `OS8`, `OS5`, `OS6`, `D14` |
| ORDER | Створення замовлення з контактними даними та отримання orderId | `DB3`, `D9`, `DB5`, `DB6` |
| ORDER_ITEM | Створення позицій, прив'язка до EDITION, фіксація quantity та priceSnapshot, обчислення вартості | `DB4`, `D10`, `D11`, `DB6`, `OS7` |
| USER | Реєстрація не є обов'язковою, створення USER не передбачено | `C1`, `C0`, `OS2` |

BOOK використовується як контекст вибору видання. AUTHOR, GENRE та PUBLISHER не деталізуються в межах оформлення замовлення.

## Уточнення та розбіжності з попередніми завданнями

| Питання | Попередні матеріали | Врахування в Завданні №4 |
|---|---|---|
| Порядок валідації | У SC-01 validateContacts() і validateItems() наведені послідовно перед спільним alt; SC-04 відхиляє запит одразу після перевірки контактів. | У `D1` передбачено раннє відхилення. Лише за наявності контактів запускається `V1`. |
| Паралельні перевірки | У SC-01 validateItems() представлено однією операцією. | У `F1`–`J1` деталізовано дві незалежні перевірки з об'єднанням результатів. |
| Актуальний залишок після rollback | У SC-01 після rollback() повертається outOfStock без доступної кількості; SC-02 і FR-11 вимагають повідомити залишок. | `DB2` накопичує insufficientEditionIds, `RB1` передає їх після rollback(); `OS8` ініціалізує актуальні залишки, `OS5` → `OS6` → `D14` повторюють перевірку для кожного ID, `E4` → `REJ3` → `MSG3` забезпечують повідомлення покупцеві. |
| Повторна спроба | У SC-02 показано можливість змінити кількість, у Gherkin UC04-S04 — виправити контакти. | `D13` дозволяє повторити оформлення після виправлення або завершити процес. |
| Передумова UC04-S03 | У Gherkin не вказано, чи заповнені контакти. | Для перевірки гілки недопустимої кількості прийнято припущення про заповнені контакти. |
| Технічні помилки | SC-01 деталізує rollback через нестачу, але не всі технічні відмови. | `E5` та `RB2` деталізують підтверджені технічні відмови. Невідомий результат commit() не змодельовано. |

Матеріали Завдань №1–3 залишаються без змін. Уточнення відображають деталізацію процесу відповідно до spec.md Завдання №4, а не нові вимоги попередніх робіт.

## Висновок

Матриця показує зв'язок усіх дев'яти функціональних вимог FR-07–FR-15 та чотирьох Gherkin-сценаріїв з конкретними вузлами однієї Activity Diagram. У моделі простежуються основний і альтернативні шляхи UC-04, учасники та повідомлення Sequence Diagram, а також сутності ER-моделі. Покриття встановлено за декларативним описом діаграми; це не замінює перевірку рендеру, коректності передавання даних або остаточний аудит.
