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

