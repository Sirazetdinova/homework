# Тестирование

## Задача 1. Тестирование программы Task Manager
    
**Цель тестирования.** Проверить корректность работы программы Task Manager, которая предназначена для управления задачами.

**Инструкция по тестированию:**

1. Запустите программу Task Manager.
2. Проверьте каждый тестовый случай, описанный ниже, с помощью автоматизированных тестов.
3. Запишите результаты тестов и заметки об ошибках, если они есть. 
    

```python
import datetime


class Task:
    def __init__(self, description, priority=1, deadline=None):
        self.description = description
        self.priority = priority
        self.deadline = deadline
        self.is_completed = False

    def mark_completed(self):
        self.is_completed = True

    def __str__(self):
        status = "Completed" if self.is_completed else "Not Completed"
        deadline_info = f"Deadline: {self.deadline}" if self.deadline else "No Deadline"
        return f"Description: {self.description}\nPriority: {self.priority}\nStatus: {status}\n{deadline_info}\n"


class TaskList:
    def __init__(self):
        self.tasks = []

    def add_task(self, task):
        self.tasks.append(task)

    def remove_task(self, task):
        self.tasks.remove(task)

    def update_task(self, task, new_description):
        if task in self.tasks:
            task.description = new_description

    def sort_by_priority(self):
        self.tasks.sort(key=lambda x: x.priority, reverse=True)

    def filter_by_status(self, completed=False):
        return [task for task in self.tasks if task.is_completed == completed]

    def set_deadline(self, task, deadline):
        task.deadline = deadline


# Пример использования
if __name__ == "__main__":
    task_list = TaskList()

    task1 = Task("Write report", priority=2)
    task_list.add_task(task1)
    task2 = Task("Buy groceries", priority=1)
    task_list.add_task(task2)
    task3 = Task("Call client", priority=3, deadline=datetime.datetime(2023, 10, 1))
    task_list.add_task(task3)

    task_list.sort_by_priority()

    print("All Tasks:")
    for task in task_list.tasks:
        print(task)

    completed_tasks = task_list.filter_by_status(completed=True)
    print("Completed Tasks:")
    for task in completed_tasks:
        print(task)

    task2.mark_completed()

    print("Updated Task List:")
    for task in task_list.tasks:
        print(task)
```

**Требования к тестам:**

1. **Тест инициализации задачи `test_task_initialization`**:
    - Создать экземпляр задачи с описанием, полученным из параметризованной фикстуры `sample_task`.
    - Убедиться, что приоритет равен 1, дедлайн не установлен (None), статус выполнения "Не выполнено" и задача не помечена как завершенная.
    
2. **Тест отметки задачи как выполненной `test_mark_completed`**:
    - Создать экземпляр задачи с описанием, полученным из параметризованной фикстуры `sample_task`.
    - Вызвать метод `mark_completed()` для того, чтобы отметить задачу как выполненную.
    - Убедиться, что статус выполнения изменился на "Выполнено", т. е. флаг задачи `is_completed` перезаписан как `True`.
    
3. **Тест строкового представления задачи `test_task_string_representation`**:
    - Создать экземпляр задачи с описанием, полученным из параметризованной фикстуры `sample_task`.
    - Убедиться, что строковое представление задачи `str(sample_task)` соответствует ожидаемому формату, который создается на основе атрибутов задачи:
      
      "Description: [описание]\n
      
       Priority: 1\n 

       Status: Not Completed\n

       No Deadline\n".
    
4. **Тест инициализации списка задач `test_tasklist_initialization`**:
    - Создать пустой список задач `TaskList`.
    - Убедиться, что список задач пуст, т. е. количество задач в списке `task_list` равно 0.
    
5. **Тест добавления задачи в список `test_add_task`**:
    - С помощью метода `add_task()` добавить задачу `sample_task` с заданным описанием "Sample Task" в список задач `task_list`.
    - Убедиться, что список содержит одну задачу, т. е. количество задач в списке `task_list` увеличилось на 1.
    - Убедиться, что  `sample_task` находится в списке задач.
    
6. **Тест удаления задач из списка `test_remove_task`**:
    - Добавить задачу с описанием, полученным из параметризованной фикстуры `sample_task`, в список задач `task_list`.
    - Вызвать метод `remove_task()` для удаления задачи `sample_task` из списка.
    - Убедиться, что после удаления задачи, количество задач в списке `task_list` уменьшилось на 1.
    - Также убедиться, что удаленная задача `sample_task` больше не присутствует в списке задач `task_list`.
    
7. **Тест сортировки задач по приоритету `test_sort_by_priority`:**
    - Добавить в список задач `task_list`  две задачи `task1` и `task2` с разными приоритетами.
    - Вызвать метод `sort_by_priority()` для сортировки задач в списке `task_list`.
    - Убедиться, что задачи в списке расположены в порядке убывания приоритета. В данной программе чем больше значение, тем выше приоритет задачи.
    
8. **Тест фильтрации задач по статусу выполнения `test_filter_by_status`:**
    - Добавить в список задач `task_list`  две задачи `task1` и `task2`. Одну из задач пометить как выполненная с помощью функции `mark_completed()`.
    - Выполнить фильтрацию задач по статусу выполнения "Выполнено" с помощью метода `filter_by_status()`.
    - Убедиться, что в результирующем списке содержится только выполненная задача т. е. количество завершенных задач равно 1.
    
9. **Тест установки дедлайна для задачи `test_set_deadline`:**
    - Создать экземпляр задачи с описанием, полученным из параметризованной фикстуры `sample_task`.
    - Установить `deadline` для задачи, используя модуль `datetime`.
    - Добавить созданную задачу в список задач `task_list` с помощью метода `add_task()`.
    - Установить дедлайн для задачи с использованием метода `set_deadline()` и передать в него созданный объект дедлайна `deadline`.
    - Проверить, что дедлайн задачи `sample_task` теперь равен установленному дедлайну `deadline`
    
***Примечание**: используйте параметризованную фикстуру `sample_task`*, которая создает экземпляр `Task` с разными описаниями задач (например, "Sample Task 1" и "Sample Task 2"). 

*А также используйте фикстуру `task_list`, которая создает экземпляр класса `TaskList`. Это позволит создавать новые списки задач для каждого теста. Таким образом, мы обеспечиваем изоляцию между тестами и удостоверяемся, что каждый тест не зависит от состояния других тестов. Это важно для корректного тестирования функциональности.*


## Задача 2. Тестирование программы Auto Watering System
    
**Цель тестирования.** Проверить корректность работы программы Automatic Watering System, которая предназначена для управления автоматической системы полива.

**Инструкция по тестированию:**

1. Запустите программу Automatic Watering System.
2. Проверьте каждый тестовый случай, описанный ниже, с помощью автоматизированных тестов.
3. Запишите результаты тестов и заметки об ошибках, если они есть. 
    

```python
import time


class AutomaticWateringSystem:
    def __init__(self, initial_water_level, initial_soil_moisture):
        self.water_level = initial_water_level
        self.soil_moisture = initial_soil_moisture
        self.is_watering = False
        self.schedule = {}

    def start_watering(self, duration_minutes, water_amount):
        if self.water_level >= water_amount:
            self.water_level -= water_amount
            self.is_watering = True
            print(f"Начался полив на {duration_minutes} минут с использованием {water_amount} мл воды.")
            print("Полив завершен.")
        else:
            self.is_watering = False
            print("Недостаточно воды для полива.")

    def add_water(self, amount):
        self.water_level += amount
        self.log_message = f"Добавлено {amount} мл воды. Текущий уровень воды: {self.water_level} мл."

    def check_soil_moisture(self):
        return self.soil_moisture

    def check_water_level(self):
        return self.water_level

    def set_watering_schedule(self, start_time, duration_minutes, water_amount):
        # Установка расписания полива
        self.schedule = {"start_time": start_time, "duration_minutes": duration_minutes, "water_amount": water_amount}
        print("Расписание полива установлено.")

    def run_scheduled_watering(self):
        # Проверка расписания и запуск полива при необходимости
        current_time = time.localtime()
        current_day = current_time.tm_wday  # Получаем текущий день недели (0 - Пн, 6 - Вс)

        if current_day in self.schedule:
            scheduled_info = self.schedule[current_day]
            start_time = scheduled_info["start_time"]
            duration_minutes = scheduled_info["duration_minutes"]
            water_amount = scheduled_info["water_amount"]

            current_hour = current_time.tm_hour
            current_minute = current_time.tm_min
            scheduled_minute = start_time // 60
            scheduled_hour = start_time % 60

            if current_hour == scheduled_hour and current_minute >= scheduled_minute:
                print(f"Запуск запланированного полива на {duration_minutes} минут.")
                self.start_watering(duration_minutes, water_amount)
                return  # Добавляем return для выхода из метода после запуска полива

# Пример использования
if __name__ == "__main__":
    watering_system = AutomaticWateringSystem(initial_water_level=1000, initial_soil_moisture=50)

    watering_system.add_water(500)

    watering_system.set_watering_schedule(start_time=8 * 60, duration_minutes=10, water_amount=200)

    print(f"Влажность почвы: {watering_system.check_soil_moisture()}%")
    print(f"Уровень воды в резервуаре: {watering_system.check_water_level()} мл")

    watering_system.run_scheduled_watering()

    print(f"Влажность почвы: {watering_system.check_soil_moisture()}%")
    print(f"Уровень воды в резервуаре: {watering_system.check_water_level()} мл")
```

**Требования к тестам:**

1. **Тест запуска полива с достаточным количеством воды `test_start_watering_with_enough_water`:**
   - Создать экземпляр системы автоматического полива с достаточным количеством воды, используя фикстуру `watering_system_with_enough_water`.
   - Вызвать метод `start_watering()` с параметрами duration_minutes=10 и water_amount. Этот шаг выполняется дважды: с water_amount=100 и water_amount=200.
   - Убедиться, что после вызова метода `start_watering()` начался полив т. е. атрибут is_watering объекта AutomaticWateringSystem равен True.

2. **Тест запуска полива с недостаточным количеством воды `test_start_watering_with_insufficient_water`:**
  - Создать экземпляр системы автоматического полива с начальным уровнем воды, используя фикстуру `watering_system_with_insufficient_water`.
  - Вызвать метод `start_watering()` с параметрами `duration_minutes=10` и `water_amount=1500`.
  - Убедиться, что после вызова метода `start_watering()` не начался полив т. е. атрибут is_watering объекта AutomaticWateringSystem равен False.

3. **Тест добавления воды `test_add_water`:**
    - Создать экземпляр системы автоматического полива с начальным уровнем воды, используя фикстуру `watering_system_with_custom_parameters`.
    - Вызвать метод `add_water()` с параметром `amount=200`.
    - Убедиться, что уровень воды увеличился до 1400 мл, используя метод check_water_level().

4. **Тест проверки уровня влажности почвы `test_check_soil_moisture`:**
  - Создать экземпляр системы автоматического полива с начальным уровнем влажности почвы, используя фикстуру `watering_system_with_custom_parameters`.
  - Убедиться, что уровень влажности равен 40, используя метод `check_soil_moisture()`.

5. **Тест установки расписания полива `test_set_watering_schedule`:**
- Создать экземпляр системы автоматического полива с пустым расписанием, используя фикстуру `watering_system_with_schedule`.
- Вызвать метод `set_watering_schedule()` с параметрами `start_time=720`, `duration_minutes=20`, и `water_amount=150`.
- Убедиться, что расписание установлено правильно, т. е. атрибут schedule содержит ожидаемые значения в словаре.

6. **Тест запуска расписанного полива, когда расписание совпадает `test_run_scheduled_watering`:**
- Создать экземпляр системы автоматического полива с установленным расписанием, используя фикстуру `watering_system_with_schedule`.
- Использовать `mocker` для имитации текущего времени. Установите текущее время с помощью mocker.patch на значение, заданное в параметре current_time. Это будет имитацией времени выполнения теста.
   -  Здесь параметр `current_time` определяет текущее время в структуре `time.struct_time`. Он задает момент времени, когда тест будет выполняться.
    - Здесь параметр `expected_is_watering` определяет ожидаемое значение атрибута `is_watering` после выполнения метода `run_scheduled_watering()`.
- Вызвать метод `run_scheduled_watering()` для объекта системы автоматического полива.
- Убедиться, что значение атрибута is_watering соответствует ожидаемому значению expected_is_watering.

  
