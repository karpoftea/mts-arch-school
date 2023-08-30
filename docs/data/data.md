# Модель предметной области
<!-- Логическая модель, содержащая бизнес-сущности предметной области, атрибуты и связи между ними. 
Подробнее: https://confluence.mts.ru/pages/viewpage.action?pageId=375782602

Используется диаграмма классов UML. Документация: https://plantuml.com/class-diagram 
-->

```plantuml
@startuml
' Логическая модель данных в варианте UML Class Diagram (альтернатива ER-диаграмме).
namespace App {
    Registration "1" o-- "0..1" User: ref
    Registration <-- RegistrationStatus: uses
    User "1" <-- "1" Role: acts
    User "1" o-- "0..*" Report: has
    Broadcast "1" o-- "1" Report: ref
    Broadcast "1" o-- "1" Room: ref
    TimeTable "1" o-- "0..*" Broadcast: ref
    Room "1" o-- "1" Chat: ref
    Room "1" o-- "0..*" User: ref
    Report "1" <-- "1" ReviewStatus: uses
    Chat "1" o-- "0..*" User: ref
    Notification "1" o-- "0..*" User: ref
    Broadcast <-- BroadcastStatus

    class TimeTable {
        Map<DateTime, Broadcast> timetable;
    }

    class Broadcast {
        DateTime startTime;
        DateTime endTime;
        BroadcastStatus status;
    }

    enum BroadcastStatus {
        ON
        OFF
    }

    class Room {
        String name;
        String url;
    }

    class Chat {
        Long id;
    }

    class Notification {
        Long id;
        String templateName;
        Map<String, Object> templateParams;
        String theme;
        String senderEmail;
        Set<String> receiverEmails;
    }

    class Registration {
        Long id;
        String name;
        String surnmame;
        String companyName;
        String jobTitle;
        String email;
        RegistrationStatus status;
    }

    class User {
        Long id;
        String name;
        String surname;
        String email;
        Role role;
    }

    class Report {
        Long id;
        String name;
        String annotation;
        ReviewStatus reviewStatus;
    }

    enum Role {
        PARTICIPANT
        REPORTER
        EXPERT
        RECRUTER
        ORGANIZER
    }

    enum RegistrationStatus {
        PENDING
        REJECTED
        ACCEPTED
    }

    enum ReviewStatus {
        PENDING
        REJECTED
        ACCEPTED
    }

}
@enduml
```
