# Компонентная архитектура
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

Person(user, "Пользователь", "Использует")
System_Boundary(service, "Сайт заказа услуг", "Обеспечивает доступ к услугам") {
    Container(user_service, "Сервис пользователей", "Java/Spring Boot", "Управление пользователями")
    Container(service_service, "Сервис услуг", "Java/Spring Boot", "Управление услугами")
    Container(order_service, "Сервис заказов", "Java/Spring Boot", "Управление заказами")
    ContainerDb(database, "База данных", "MySQL", "Хранение данных о пользователях, услугах и заказах")
}

Rel(user, user_service, "Создание нового пользователя")
Rel(user, user_service, "Поиск пользователя по логину")
Rel(user, user_service, "Поиск пользователя по маске имени и фамилии")

Rel(user, service_service, "Создание услуги")
Rel(user, service_service, "Получение списка услуг")

Rel(user, order_service, "Добавление услуг в заказ")
Rel(user, order_service, "Получение заказа для пользователя")

Rel(user_service, database, "INSERT/SELECT/UPDATE")
Rel(service_service, database, "INSERT/SELECT/UPDATE")
Rel(order_service, database, "INSERT/SELECT/UPDATE")

@enduml

## Список компонентов  

### Сервис пользоватлей
**API**:
     - Создание нового пользователя
     - Поиск пользователя по логину
     - Поиск пользователя по маске имени и фамилии

### Сервис услуг
**API**:
     - Создание услуги
     - Получение списка услуг

### Сервис заказов

**API**:
     - Добавление услуг в заказ
     - Получение заказа для пользователя