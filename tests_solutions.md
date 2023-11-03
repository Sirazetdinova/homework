# Тестирование

## Задача 1. Тестирование программы Task Manager
     
```python
import pytest
import datetime

from app.task_manager import Task, TaskList


# Фикстура для создания экземпляра TaskList
@pytest.fixture
def task_list():
    return TaskList()


# Параметризованная фикстура для создания экземпляра Task
@pytest.fixture(params=["Sample Task 1", "Sample Task 2"])
def sample_task(request):
    return Task(request.param)


# Тест инициализации экземпляра Task
def test_task_initialization(sample_task):
    assert sample_task.description.startswith("Sample Task")
    assert sample_task.priority == 1
    assert sample_task.deadline is None
    assert not sample_task.is_completed


# Тест работы метода mark_completed
def test_mark_completed(sample_task):
    sample_task.mark_completed()
    assert sample_task.is_completed


# Тест строкового представления задачи
def test_task_string_representation(sample_task):
    expected_string = f"Description: {sample_task.description}\nPriority: 1\nStatus: Not Completed\nNo Deadline\n"
    assert str(sample_task) == expected_string


# Тест инициализации экземпляра TaskList
def test_tasklist_initialization(task_list):
    assert len(task_list.tasks) == 0


# Тест добавления задачи в список задач
def test_add_task(task_list, sample_task):
    task_list.add_task(sample_task)
    assert len(task_list.tasks) == 1
    assert sample_task in task_list.tasks


# Тест удаления задачи из списка задач
def test_remove_task(task_list, sample_task):
    task_list.add_task(sample_task)
    task_list.remove_task(sample_task)
    assert len(task_list.tasks) == 0
    assert sample_task not in task_list.tasks


# Тест сортировки задач по приоритету
def test_sort_by_priority(task_list):
    task1 = Task("High Priority Task", priority=3)
    task2 = Task("Low Priority Task", priority=1)
    task_list.add_task(task1)
    task_list.add_task(task2)
    task_list.sort_by_priority()
    assert task_list.tasks == [task1, task2]


# Тест фильтрации задач по статусу выполнения
def test_filter_by_status(task_list):
    task1 = Task("Completed Task")
    task2 = Task("Not Completed Task")
    task1.mark_completed()
    task_list.add_task(task1)
    task_list.add_task(task2)
    completed_tasks = task_list.filter_by_status(completed=True)
    assert len(completed_tasks) == 1
    assert task1 in completed_tasks


# Тест установки срока задачи
def test_set_deadline(task_list, sample_task):
    deadline = datetime.datetime(2023, 10, 1)
    task_list.add_task(sample_task)
    task_list.set_deadline(sample_task, deadline)
    assert sample_task.deadline == deadline
```


## Задача 2. Тестирование программы Watering System
     

```python
import pytest
from app.watering_system import WateringSystem


@pytest.fixture
def watering_system():
    system = WateringSystem()
    system.add_area("Газон", 30)
    system.water_spray_supply("Газон", 10)
    system.add_area("Клумба", 25)
    system.water_spray_supply("Клумба", 8)
    return system


# Тест начального уровня влажности участка
def test_initial_soil_moisture(watering_system):
    assert watering_system.areas["Газон"]["soil_moisture"] == 30


# Тест добавления воды в систему
def test_add_water(watering_system):
    watering_system.add_water(500)
    assert watering_system.water_level == 2500


# Тест добавления уже существующего участка
def test_add_existing_area(watering_system):
    result = watering_system.add_area("Газон", 50)
    assert result is None
    assert watering_system.areas["Газон"]["soil_moisture"] == 30  # Уровень влажности не изменился


# Тест добавления нового участка
def test_add_new_area(watering_system):
    result = watering_system.add_area("Сад", 40)
    assert result is None
    assert "Сад" in watering_system.areas


# Тест установки расписания полива
def test_water_spray_supply(watering_system):
    watering_system.test_water_spray_supply("Газон", 15)
    assert watering_system.areas["Газон"]["spray_water"] == 15


# Параметризованный тест для проверки уровня влажности после полива
@pytest.mark.parametrize(
    "area, duration, expected_moisture",
    [
        ("Газон", 30, 100),  # Полив Газона на 30 минут, ожидается 100% влажности
        ("Клумба", 20, 100),  # Полив Клумбы на 20 минут, ожидается 100% влажности
    ],
)
def test_water_area(watering_system, area, duration, expected_moisture):
    watering_system.water_area(area, duration)
    moisture = watering_system.areas[area]["soil_moisture"]
    assert moisture == expected_moisture


# Тест на полив при нехватке воды
def test_water_area_not_enough_water(watering_system):
    watering_system.water_level = 0  # Минимальный уровень воды
    result = watering_system.water_area("Газон", 30)
    assert result is None  # Ожидаем, что метод возвращает None


def test_max_soil_moisture(watering_system):
    watering_system.areas["Газон"][
        "soil_moisture"
    ] = 100  # Устанавливаем максимальную влажность
    result = watering_system.water_area("Газон", 30)
    assert (
            result is None
    )  # Ожидаем, что не будет полива, так как влажность уже максимальная


# Тест влажности почвы после длительного полива
def test_soil_moisture_after_long_watering(watering_system):
    watering_system.water_area("Газон", 60)
    moisture = watering_system.areas["Газон"]["soil_moisture"]
    assert (
            moisture == 100
    )  # Ожидаем, что влажность станет максимальной


# Тест полива без включения системы
def test_watering_without_starting(watering_system):
    watering_system.stop_watering() 
    result = watering_system.water_area("Газон", 30)
    assert result is None  # Ожидаем, что не будет полива, так как система не включена


# Тест уровня влажности после полива
def test_soil_moisture_after_watering(watering_system):
    watering_system.water_area("Газон", 30)
    assert watering_system.areas["Газон"]["soil_moisture"] == 100  # Ожидаем, что уровень влажности стал 100%

```

