# Документация к KPTC SCHEDULE API
# Подключение

Адрес для выполнения методов API:
`http://sinus44.mooo.com/`

---

# Структура запросов

Для API на данный момент используются только GET - методы
Указание аргументов: `{api_link}/method?param1=value1` 
Пример: `http://sinus44.mooo.com/getDayCalls?day=0`

Для передачи списка элементов, использовать "," в качестве разделителя.
Пример: `http://sinus44.mooo.com/getScheduleDateList?dates=16.09.2024,17.09.2024,18.09.2024`

---

# Общее
### Enum WEEK_DAY_INDEX
- 0 `Понедельник`
- 1 `Вторник`
- 2 `Среда` 
- 3 `Четверг`
- 4 `Пятница`
- 5 `Суббота`


## Методы
- `ping()` - Возвращает случайное число, предназначено для тестирования
---

# Звонки
### Enum INTERVAL_TYPE
- 0 `LESSON`           - Пара
- 1 `LITTLE_CHANGE`    - Маленькая перемена между парами
- 2 `MIDDLE_CHANGE`    - Средняя перемена (между 1й и 2й парой)
- 3 `BIG_CHANGE`       - Большая перемена (Обед)
- 4 `CONVERSATIONS`    - Разговоры о важном
- 5 `LESSON_CHANGE`    - Перемена между частями пар

### class Call
Класс для описания одного интервала времени 
- `time_start: str`     - Время начала интервала (например "08:15")
- `time_end: str`       - Время конца интервала (например "09:00")
- `type: INTERVAL_TYPE` - Тип интервала (например INTERVAL_TYPE.LESSON)

## Методы

- `getAllCalls()`                          - Всё расписание звонков
- `getDayCalls(day: WEEK_DAY_INDEX)`       - Получить расписание звонков на определенный день недели
- `getDayLessonCalls(day: WEEK_DAY_INDEX)` - Получить только время пар на определенный день недели

---

# Файлы

### Class File
Класс описывающий Google-файл
- `date`           - Дата на которую предназначено расписание
- `full_name`      - Полное название файла включая расширение
- `id`             - ID файла (google file id)
- `last_update`    - Последнее обновление файла на гугл диске
- `name`           - Название файла без расширения
- `week_day_index` - Индекс дня недели
- `week_day_name`  - Название дня недели*

### Методы:
- `getAvailableFiles()`     - Получить все доступные файлы с гугл диска
- `getActualFiles()`        - Получить только актуальные (по дате предназначения) файлы
- `getFileDate(date: str)`  - Получить файл по дате
- `getFileID(file_id: str)` - Получить файл по ID
---

# Расписание

### Class Schedule
Расписание на один день
- `groups: list[Group]` - Список расписаний конкретных групп
- `file: File`          - Файл из которого производился парсинг

### Class Group
Расписание на один день для одной группы
- `char: int`             - Буква в имени группы (1-1а9 -> char = "а")
- `course: int`           - Номер курса (3-1п9 -> course = 3)
- `full_name: str`        - Полное название группы
- `sub_course: int`       - Номер подгруппы (3-1п9 -> sub_course = 1)
- `year: int`             - После скольки лет обучения в школе поступили (допустимые значения 9 или 11) (3-1п9 -> year = 9)
- `lessons: list[Lesson]` - Список занятий  

### Class Lesson
Описание одного занятия одной группы
- `classroom: str`     - Кабинет (например "220 каб.")
- `classroom_raw: str` - Кабинет, но так же как написано в файле-оригинале (например "220")
- `discipline: str`    - Название дисциплины (например "История")
- `index: int`         - Номер пары (1 - первая пара, 2 - вторая пара и т.д.)
- `postfix`            - Постфикс для кабинета (например "каб.")
- `time`               - Время пары

### Методы
- `getScheduleDay(file_id: str) -> list[Group]`               - Получить расписание на день по ID файла
- `getScheduleDate(date: str) -> list[Group]`                 - Получить расписание на день по дате
- `getScheduleDays(file_ids: list[str]) -> list[Schedule]`    - Получить список расписаний по списку ID файлов
- `getScheduleDates(dates: list[str]) -> list[Schedule]`      - Получить список расписаний по списку дат *
- `getAllSchedule() -> list[Schedule]`                        - Получить всё доступное расписание *      
- `getActualSchedule() -> list[Schedule]`                     - Получить актуальное расписание (на сегодня или в будущем) *

---

# Обновления расписания
Планируется добавить возможность получения изменений с помощью webhooks и callback
### Enum Update_Type
- 0 `NEW`  - Добавлен новый файл
- 1 `EDIT` - Редактирован старый файл

### Class Update
- `update_type: Update_Type` - Тип обновления
- `files_id: str` - Идентификатор обновленного файла 

### Callback*
- `getUpdates(offset: int)` - Возвращает обновления начиная с определенного смещения *
- `getLastUpdateId() -> update_id` - Возвращает ID последнего обновления *

### Webhooks*
Для использования WebHooks будет необходима "Регистрация", а создание вебхуков будет доступно только по полученому токену

- `webhookRegisterToken(name, pass) -> token` - ... *
- `webhookCreate(token, callback_addr) -> webhook` - ...*
- `webhookDelete(token, webhook_id)` *

---

\* Реализация планируется
