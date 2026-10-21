# REST API SimBank (учебная модель)

| Операция | Метод и адрес | Тело / параметры | Успех | Ошибки | Кто может |
|---|---|---|---|---|---|
| Список своих счетов | `GET /accounts` | — | 200 | 401 | Клиент |
| Баланс счёта | `GET /accounts/{accountId}/balance` | — | 200 | 401, 404 | Владелец счёта |
| История операций | `GET /accounts/{accountId}/transactions?limit=20&offset=0` | query | 200 | 400, 401, 404 | Владелец счёта |
| Создать перевод | `POST /transfers` | `sourceAccountId`, `destinationAccount`, `amount`, `currency` | 201 | 400, 401, 404, 409 | Клиент |
| Статус перевода | `GET /transfers/{transferId}` | — | 200 | 401, 404 | Создатель перевода |
| Отменить перевод до обработки | `POST /transfers/{transferId}/cancel` | — | 200 | 401, 404, 409 | Создатель перевода |
| Список обращений | `GET /support/tickets` | `status` optional | 200 | 401, 403 | Поддержка |
| Изменить обращение | `PATCH /support/tickets/{ticketId}` | `status` | 200 | 400, 403, 404 | Поддержка |

## Связь API с классами
`Account`, `Transaction` и `Transfer` становятся ресурсами API: у них есть идентификаторы и операции. `TransferService` не является ресурсом, поскольку это внутренняя бизнес-логика. `User` не раскрывается напрямую, чтобы не выдавать лишние персональные данные.
