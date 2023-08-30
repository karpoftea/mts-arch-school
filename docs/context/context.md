# Контекст решения
<!-- Окружение системы (роли, участники, внешние системы) и связи системы с ним. Диаграмма контекста C4 и текстовое описание. 
Подробнее: https://confluence.mts.ru/pages/viewpage.action?pageId=375783261
-->
```plantuml
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

LAYOUT_WITH_LEGEND()

Person(participant, "Участник", "Посещает доклады, оставляет обратную связь")
Person(reporter, "Докладчик", "Представляет доклады участникам конференции")
Person(export, "Эксперт", "Ревьюит доклады конференции")
Person(organizer, "Организатор", "Ответсвенный за управление всеми аспектами конференции")
Person(recruter, "Рекрутер", "Работает информацией о кандидатах")

System(confsys, "МТС HelloConf", "Система реализующая управление веб-конференцией МТС HelloConf")

System_Ext(emailsys, "Система рассылки e-mail", "Отправляет/получает email-ы, доставляет их до пользователей")
System_Ext(vspsys, "Система видео-стриминга", "Управляет стримингом видео, его записью и хранением")

Rel(participant, confsys, "Регистрируется, просматривает расписание")
Rel(reporter, confsys,  "Регистрируется, предоставляет доклад")
Rel(export, confsys,  "Рецензирует доклад")
Rel(organizer, confsys,  "Управляет расписанием конференции, рассылками")
Rel(recruter, confsys,  "Получает отчеты об участниках")

Rel(confsys, emailsys, "Отправляет email-ы", "smtp")
Rel(confsys, vspsys, "Управляет стримингом", "tcp")
Rel(participant, vspsys, "Подключается к вещанию", "tcp")
Rel(reporter, vspsys, "Подключается к вещанию", "tcp")
Rel(emailsys, participant, "Доставляет email", "smtp")
Rel(emailsys, reporter, "Доставляет email", "smtp")
@enduml
```
