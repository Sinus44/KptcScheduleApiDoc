# Список изменений
- 0.0.6(_05.10.2024_):
- - [FIXED] [API] [CALLS] Исправлена внутреняя ошибка которая возникала, когда не было найдено расписание звонков для определенной пары (например: нет расписания звонков для 5й пары в субботу)
- 0.0.5(_03.10.2024_):
- - [FIXED] [API] [SCHEDULE] Исправлена внутреняя ошибка которая возникала, когда хотя бы у одной из групп было более 5 пар за день
- 0.0.4 (_20.09.2024_):
- - [ADDED] [API] [FILE] Добавлен метод "getFileID" для получения файла по ID
- - [ADDED] [API] [SCHEDULE] Добавлен метод "getScheduleDays" для получения списка файлов по идентификаторам
- - [ADDED] [API] [SCHEDULE] У объектов класса "Lesson" теперь указывается время пары
- - [ADDED] [API] [SCHEDULE] Добавлен класс "Schedule" описывающий расписание на 1 день 
- - [ADDED] [DOC] Добавлено пояснение для передачи списка
- - [FIXED] [API] [SCHEDULE] Методы "getScheduleDays" и "getSchedule" теперь возвращают объект класса "Schedule" и "list[Schedule]" соответсвенно 
- - [FIXED] [API] [SCHEDULE] Свойство "index" класса "Lesson" имело ошибочный тип "str" исправлено на "int"
- 0.0.3 (_16.09.2024_):
- - [ADDED] [API] [FILE] Добавлен метод "getFileDate(date: str)" для получения файла по дате
- - [ADDED] [API] [SCHEDULE] Добавлен метод "getScheduleDate(date: str)" для получения расписания по дате
- - [ADDED] [DOC] [SCHEDULE] Добавлено описание классов "Group" и "Lesson"
- - [FIXED] [DOC] Мелкие правки документации, добавление анотации типов, в т.ч. возвращаемых типов
- 0.0.2 (_14.09.2024_): 
- - [ADDED] [API] [FILE] Добавлено свойство "week_day_index" для "File"
- - [ADDED] [API] [PING] Добавлен метод "ping" для проверки API на работоспособность
- - [FIXED] [DOC] Исправление документации "getSheduleDay" -> "getScheduleDay" 
