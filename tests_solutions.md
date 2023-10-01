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


# Тесты для класса Task
def test_task_initialization(sample_task):
    assert sample_task.description.startswith("Sample Task")
    assert sample_task.priority == 1
    assert sample_task.deadline is None
    assert not sample_task.is_completed


def test_mark_completed(sample_task):
    sample_task.mark_completed()
    assert sample_task.is_completed


def test_task_string_representation(sample_task):
    expected_string = f"Description: {sample_task.description}\nPriority: 1\nStatus: Not Completed\nNo Deadline\n"
    assert str(sample_task) == expected_string


# Тесты для класса TaskList
def test_tasklist_initialization(task_list):
    assert len(task_list.tasks) == 0


def test_add_task(task_list, sample_task):
    task_list.add_task(sample_task)
    assert len(task_list.tasks) == 1
    assert sample_task in task_list.tasks


def test_remove_task(task_list, sample_task):
    task_list.add_task(sample_task)
    task_list.remove_task(sample_task)
    assert len(task_list.tasks) == 0
    assert sample_task not in task_list.tasks


def test_sort_by_priority(task_list):
    task1 = Task("High Priority Task", priority=3)
    task2 = Task("Low Priority Task", priority=1)
    task_list.add_task(task1)
    task_list.add_task(task2)
    task_list.sort_by_priority()
    assert task_list.tasks == [task1, task2]


def test_filter_by_status(task_list):
    task1 = Task("Completed Task")
    task2 = Task("Not Completed Task")
    task1.mark_completed()
    task_list.add_task(task1)
    task_list.add_task(task2)
    completed_tasks = task_list.filter_by_status(completed=True)
    assert len(completed_tasks) == 1
    assert task1 in completed_tasks


def test_set_deadline(task_list, sample_task):
    deadline = datetime.datetime(2023, 10, 1)
    task_list.add_task(sample_task)
    task_list.set_deadline(sample_task, deadline)
    assert sample_task.deadline == deadline
```


## Задача 2. Тестирование программы Auto Watering System
     

```python
import pytest
from app.watering_system import AutomaticWateringSystem
import time

@pytest.fixture
def watering_system_with_enough_water():
    return AutomaticWateringSystem(initial_water_level=1000, initial_soil_moisture=50)

@pytest.fixture
def watering_system_with_insufficient_water():
    return AutomaticWateringSystem(initial_water_level=500, initial_soil_moisture=50)

@pytest.fixture
def watering_system_with_custom_parameters():
    return AutomaticWateringSystem(initial_water_level=1200, initial_soil_moisture=40)

@pytest.fixture
def watering_system_with_schedule():
    system = AutomaticWateringSystem(initial_water_level=1000, initial_soil_moisture=50)
    system.set_watering_schedule(start_time=720, duration_minutes=20, water_amount=150)
    return system

@pytest.mark.parametrize("water_amount", [100, 200])
def test_start_watering(watering_system_with_enough_water, water_amount):
    watering_system_with_enough_water.start_watering(duration_minutes=10, water_amount=water_amount)
    assert watering_system_with_enough_water.is_watering is True

def test_start_watering_with_insufficient_water(watering_system_with_insufficient_water):
    watering_system_with_insufficient_water.start_watering(duration_minutes=10, water_amount=1500)
    assert watering_system_with_insufficient_water.is_watering is False

def test_add_water(watering_system_with_custom_parameters):
    watering_system_with_custom_parameters.add_water(200)
    assert watering_system_with_custom_parameters.check_water_level() == 1400

def test_check_soil_moisture(watering_system_with_custom_parameters):
    assert watering_system_with_custom_parameters.check_soil_moisture() == 40

def test_set_watering_schedule(watering_system_with_schedule):
    assert watering_system_with_schedule.schedule == {"start_time": 720, "duration_minutes": 20, "water_amount": 150}

@pytest.mark.parametrize("current_time, expected_is_watering", [
    (time.struct_time((2023, 10, 1, 12, 0, 0, 0, 274, 0)), False),
    (time.struct_time((2023, 10, 1, 12, 30, 0, 0, 274, 0)), False),
])
def test_run_scheduled_watering(watering_system_with_schedule, mocker, current_time, expected_is_watering):
    mocker.patch('time.localtime', return_value=current_time)
    watering_system_with_schedule.run_scheduled_watering()
    assert watering_system_with_schedule.is_watering == expected_is_watering
```















