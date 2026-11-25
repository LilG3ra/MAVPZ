# Sequence Diagram — SC-01 Успішне оформлення замовлення

## Опис

Ця діаграма деталізує успішне оформлення замовлення в онлайн-магазині друкованих книг (UC-04 із Завдання №2). Вона показує взаємодію покупця, інтерфейсу, сервісів та сховища даних, а саме: від надсилання замовлення до підтвердження, включно з перевіркою даних, залишків видань і фіксацією ціни.

## Діаграма

```mermaid
sequenceDiagram
    actor Customer as Customer
    participant UI as OrderUI
    participant OrderService as OrderService
    participant StockService as StockService
    participant Database as Database

    Customer->>UI: selectEditions(editions[], quantities[])
    UI->>UI: displaySelectedBooks()
    Customer->>UI: enterContactData(contactData)
    Customer->>UI: submitOrder()
    activate UI

    UI->>OrderService: submitOrder(contactData, items[])
    activate OrderService

    OrderService->>OrderService: validateContacts(contactData)
    OrderService->>OrderService: validateItems(items[])
    Note over OrderService: At least one item and all quantities > 0

    alt Invalid contacts or items
        OrderService-->>UI: orderRejected(validationError)
        UI-->>Customer: showValidationError()
    else Valid input
        OrderService->>OrderService: aggregateItemsByEdition(items[])
        Note over OrderService: allAvailable = true

        loop For each requested edition
            OrderService->>StockService: checkStock(editionId, totalQuantity)
            activate StockService
            StockService->>Database: queryEditionStock(editionId)
            activate Database
            Database-->>StockService: available
            deactivate Database
            StockService-->>OrderService: stockCheck(available >= totalQuantity)
            deactivate StockService
            Note over OrderService: Update allAvailable
        end

        alt Insufficient stock for any edition
            OrderService-->>UI: orderRejected(outOfStock)
            UI-->>Customer: showOutOfStockError()
            Note over OrderService: ORDER and ORDER_ITEM are not created
        else All editions available
            OrderService->>Database: createOrderAtomically(contactData, items[])
            activate Database
            Database->>Database: beginTransaction()
            Note over Database: transactionalStockValid = true

            loop For each requested edition
                Database->>Database: lockEditionAndReadStockAndPrice()
                Note over Database: Check totalQuantity and capture priceSnapshot
                Note over Database: Update transactionalStockValid
            end

            alt Stock changed or insufficient
                Database->>Database: rollback()
                Database-->>OrderService: orderRejected(outOfStock)
            else All quantities available
                Database->>Database: createOrderRecord(contactData)
                Note over Database: Generated orderId

                loop For each order item
                    Database->>Database: createOrderItem(orderId, editionId, quantity, priceSnapshot)
                    Database->>Database: updateEditionStock(editionId, quantity)
                end

                Database->>Database: commit()
                Database-->>OrderService: orderCreated(orderId, summary)
            end
            deactivate Database

            alt Order successfully saved
                OrderService-->>UI: orderCreated(orderId, summary)
                UI-->>Customer: confirmationMessage(orderId, summary)
            else Transaction rolled back
                OrderService-->>UI: orderRejected(outOfStock)
                UI-->>Customer: showOutOfStockError()
            end
        end
    end

    deactivate OrderService
    deactivate UI
```

[Вихідний код Mermaid](https://github.com/LilG3ra/MAVPZ/blob/main/task-3-sequence-diagram/diagrams/SC-01.mmd)

[Відкрити Mermaid](https://mermaid.live/)

[Матриця трасування](../traceability.md) - ще не готово

## Основні учасники

- Customer — обирає видання, зазначає кількість, вводить контактні дані та підтверджує замовлення.
- OrderUI — приймає дані та показує результат оформлення.
- OrderService — перевіряє замовлення, координує перевірку залишків і створення записів.
- StockService — перевіряє доступний залишок вибраного видання.
- Database — надає дані про видання та виконує транзакційне збереження замовлення, його позицій і змін залишків.

## Основні кроки взаємодії

- Покупець обирає видання та вказує кількість, заповнює контакти й надсилає замовлення.
- OrderService виконує validateContacts() і validateItems(): замовлення має містити хоча б одну позицію, а кількість кожної позиції має бути додатною.
- OrderService групує однакові видання та через StockService перевіряє, чи достатньо примірників для всіх позицій.
- За успішної перевірки Database починає транзакцію, повторно перевіряє залишки та зчитує актуальні ціни видань.
- Database створює ORDER, пов’язані ORDER_ITEM з orderId та priceSnapshot, оновлює залишки й завершує транзакцію.
- OrderService передає результат інтерфейсу, який показує покупцеві підтвердження.

## Зв'язки між учасниками

- Customer взаємодіє з OrderUI, а не з самою базою даних.
- OrderUI передає запит на оформлення до OrderService.
- OrderService звертається до StockService, а StockService до Database.
- Створення ORDER і ORDER_ITEM та оновлення залишків показані всередині однієї транзакції.
- Фрагменти loop моделюють обробку кожного видання й позиції, а фрагменти alt — успішні та помилкові результати перевірок.

## Основні бізнес-правила

- Замовлення можна оформлювати без обов’язкової реєстрації.
- У замовленні має бути щонайменше одна позиція, а її кількість повинна бути більшою за нуль.
- Кожна позиція ORDER_ITEM стосується конкретного EDITION та пов’язана із замовленням ORDER через orderId.
- Сумарна замовлена кількість одного видання не повинна перевищувати залишок.
- Ціна фіксується як priceSnapshot на момент оформлення.
- У разі відхилення транзакції замовлення не повинно зберігатися частково.

## Висновок

Діаграма деталізує успішний шлях UC-04 та враховує перевірку даних, залишків, створення ORDER і ORDER_ITEM і фіксацію ціни. Альтернативні помилкові сценарії деталізовані окремо в SC-02 - SC-04.
