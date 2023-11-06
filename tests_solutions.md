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
class WateringSystem:
    def __init__(self):
        self.water_level = 2000  # Начальный уровень воды в системе
        self.is_watering = False  # Флаг, указывающий, идет ли полив в данный момент
        self.areas = {}  # Возможные участки для полива

    @property
    def water_level(self):
        return self._water_level

    @water_level.setter
    def water_level(self, value):
        self._water_level = value

    @property
    def is_watering(self):
        return self._is_watering

    @is_watering.setter
    def is_watering(self, value):
        self._is_watering = value

    def get_water_level(self):
        print(f"Current water level in the system: {self.water_level} мл \n")

    # Добавление воды в систему
    def add_water(self, amount):
        self.water_level += amount

    # Добавление нового участка для полива
    def add_area(self, area, initial_moisture):
        if area not in self.areas:
            self.areas[area] = {
                "soil_moisture": initial_moisture,  # Уровень влажности почвы на участке
                "spray_water": 0,  # Скорость подачи воды
            }
        else:
            print(f"An area named {area} already exists in the system.")

    def check_soil_moisture(self, area_name=None):
        if area_name is not None:
            if area_name in self.areas:
                moisture = self.areas[area_name]["soil_moisture"]
                print(f"Moisture level for area {area_name}: {moisture}%.")
            else:
                print(f"An area named {area_name} already exists in the system.")
        else:
            for area, data in self.areas.items():
                moisture = data["soil_moisture"]
                print(f"Moisture level for area {area_name}: {moisture}%.")

    # Полив участка на некоторое время
    def water_area(self, area, duration):
        if area in self.areas:
            if self.is_watering:
                print("Watering is already in progress. Wait for the current watering to complete.")
                return  # Останавливаем выполнение метода
            print(f"Watering of the {area} has been started.")
            self.is_watering = True  # Включаем систему полива
            water_needed = (
                duration * self.areas[area]["spray_water"]
            )  # Вычисляем необходимое количество воды
            if self.water_level >= water_needed:
                if self.areas[area]["soil_moisture"] < 100:
                    # Если уровень влажности на участке не достиг 100%
                    self.water_level -= water_needed
                    new_soil_moisture = self.areas[area]["soil_moisture"] + (
                        duration * 5
                    )
                    self.areas[area]["soil_moisture"] = min(
                        new_soil_moisture, 100
                    )  # Ограничиваем влажность до 100%
                else:
                    print(
                        f"Zone {area} already has maximum moisture (100%) and does not require watering."
                    )
            else:
                print(f"Not enough water to spray the area {area}")
            print(f"The watering of the {area} has been completed.")
            self.is_watering = False  # Выключаем систему полива

    # Подача воды для участка
    def water_spray_supply(self, area, spray_water):
        if area in self.areas:
            self.areas[area]["spray_water"] = spray_water
        else:
            print(
                f"Area named {area} does not exist in the system. Please add a site using add_area."
            )


if __name__ == "__main__":
    system = WateringSystem()

    system.get_water_level()

    system.add_area("Garden", 30)
    system.check_soil_moisture("Garden")
    system.water_spray_supply("Garden", 10)
    system.water_area("Garden", 30)
    system.check_soil_moisture("Garden")

    system.get_water_level()

    system.add_area("Flowerbed", 25)
    system.check_soil_moisture("Flowerbed")
    system.water_spray_supply("Flowerbed", 8)
    system.water_area("Flowerbed", 20)
    system.check_soil_moisture("Flowerbed")

    system.get_water_level()
```

