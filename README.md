# Train-tickets

Проект в рамках тестового задания, необходимо было разработать сервис для покупки билетов.
Время на разработку ~неделя.
Используемые технологии:
- Spring
- Hibernate
- H2-in-mem
- Rest-сервисы на Json 

Структура проекта состоит из след. лейеров:

- DAO
- Model
- Controller (Rest)
- Config

Для построения архитектуры БД, выделено 2 сущности:

- билет (ticket)
- маршрут (route)


Билет (ticket) имеет внешний ключ
к маршруту (route) как (Many-to-One)

При создании маршрута, генерируется лист билетов,
который впоследствии может быть модифицирован, использованием метода buyTicket().

Предполагается такой порядок взаимодействия через Rest-сервисы:
1. Создается маршрут (метод addRoute). У каждого билета есть поле purchased, по умолчанию false.
2. Маршруты можно запросить по дате (метод findRoutesByDate).
3. Далее взаимодйствие происходит через id маршрута. 
 * Можно вызвать либо getPurchasedTickets и посмотреть все купленные билеты.
 * Использовать getAvailableTickets и узнать о доступных билетах.
4. Чтобы приобрести билет(buyTicket), нужно знать id доступного билета и маршрута.
После вызова, состояние поля purchased меняется, и теперь данный билет недоступен при вызове getPurchasedTickets.
