# Sequence Diagram — SC-01 Успішне оформлення замовлення

## Опис

Ця діаграма деталізує успішне оформлення замовлення в онлайн-магазині друкованих книг (UC-04 із Завдання №2). Вона показує взаємодію покупця, інтерфейсу, сервісів і сховища даних: від надсилання замовлення до підтвердження, включно з перевіркою даних і залишків, транзакційним збереженням, фіксацією ціни та розрахунком вартості позицій.

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
                    Database->>Database: calculateItemTotal(quantity, priceSnapshot)
                    Note over Database: itemTotal = quantity * priceSnapshot
                    Database->>Database: createOrderItem(orderId, editionId, quantity, priceSnapshot)
                    Database->>Database: updateEditionStock(editionId, quantity)
                end

                Database->>Database: commit()
                Database-->>OrderService: orderCreated(orderId, savedItems[])
                Note over OrderService: savedItems contain quantity, priceSnapshot and itemTotal
            end
            deactivate Database

            alt Order successfully saved
                OrderService->>OrderService: initializeOrderSummary(orderId)

                loop For each saved order item
                    OrderService->>OrderService: addItemToSummary(editionId, quantity, priceSnapshot, itemTotal)
                end

                OrderService-->>UI: orderCreated(orderId, summary)
                UI-->>Customer: confirmationMessage(orderId, summary)
                Note over UI,Customer: Summary shows quantity, unit price and item total
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

[Відкрити Mermaid Live](https://mermaid.live/)

[Матриця трасування](../traceability.md)

## Основні учасники

- **Customer** — обирає видання, зазначає кількість, вводить контактні дані та підтверджує замовлення.
- **OrderUI** — приймає дані й показує результат оформлення та підсумок замовлення.
- **OrderService** — перевіряє дані, координує перевірку залишків і створення замовлення, формує підсумок із збережених позицій.
- **StockService** — перевіряє доступні залишки обраних видань.
- **Database** — надає інформацію про видання, транзакційно створює замовлення та позиції, фіксує ціни, обчислює вартість позицій і оновлює залишки.

## Основні кроки взаємодії

- Покупець обирає видання та кількість, заповнює контакти й надсилає замовлення.
- OrderService виконує validateContacts() і validateItems(): замовлення містить щонайменше одну позицію, кількість кожної позиції додатна.
- OrderService групує позиції за виданням і через StockService перевіряє достатність залишків.
- Database розпочинає транзакцію, блокує відповідні видання, повторно перевіряє залишки й фіксує актуальну ціну як priceSnapshot.
- Database створює ORDER та пов'язані ORDER_ITEM, обчислює itemTotal = quantity * priceSnapshot, оновлює залишки й виконує commit(); якщо залишку недостатньо, виконує rollback().
- Після успішного збереження Database повертає OrderService ідентифікатор замовлення та savedItems[] із кількістю, ціною та вартістю позицій.
- OrderService формує summary через initializeOrderSummary() та addItemToSummary(), після чого OrderUI показує покупцеві підтвердження з кількістю, ціною одиниці й сумою позиції.

## Зв'язки між учасниками

- Customer взаємодіє з OrderUI, а не безпосередньо з базою даних.
- OrderUI передає запит до OrderService.
- OrderService звертається до StockService, а StockService читає залишки з Database.
- Створення ORDER і ORDER_ITEM, обчислення вартості позицій та оновлення залишків виконуються в межах транзакції Database.
- Формування підсумку замовлення належить OrderService, який використовує збережені дані після успішного commit().
- Фрагменти loop моделюють обробку видань і позицій, а alt — успішні та помилкові результати перевірок.

## Основні бізнес-правила

- Замовлення можна оформити без обов'язкової реєстрації.
- Замовлення повинно містити щонайменше одну позицію, а кількість кожної позиції має бути більшою за нуль.
- Кожна позиція ORDER_ITEM стосується конкретного EDITION і пов'язана з ORDER через orderId.
- Сумарна замовлена кількість одного видання не може перевищувати доступний залишок.
- Ціна одиниці фіксується як priceSnapshot на момент оформлення; вартість позиції дорівнює quantity * priceSnapshot (FR-14).
- У разі rollback() замовлення не повинно зберігатися частково.

## Висновок

SC-01 деталізує успішний шлях UC-04, включно з перевіркою даних та залишків, атомарним створенням ORDER і ORDER_ITEM, фіксацією ціни, обчисленням вартості позицій і формуванням підтвердження. Помилкові сценарії окремо деталізовано в SC-02–SC-04.
