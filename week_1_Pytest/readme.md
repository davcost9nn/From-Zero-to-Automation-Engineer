День	Тема	                                                Задачи	                                                                                         Коммиты в GitHub
1	Установка и базовые тесты	    Настройка окружения, первые тесты.	                                    feat: add basic pytest tests
2	Фикстуры	                      Создание фикстур для данных и браузеров.	                                    feat: implement fixtures
3	Параметризация тестов	    Написание параметризованных тестов для разных сценариев.	feat: add parametrized tests
4	Обработка исключений	    Тестирование ошибок и исключений.	                                    feat: exception handling tests
5	Генерация отчётов	                     Настройка Allure/HTML-отчётов.	                                                     docs: add pytest-html reports
6	Интеграция с GitHub Actions	    Автоматизация запуска тестов при пуше.	                                   ci: update GitHub Actions workflow
7	Повторение и проект	    Итоговый проект: тесты для калькулятора + отчет.	                  feat: final week 1 project


Подробно по дням
День 1 (26.04): Установка и базовые тесты
Теория:

Установите pytest: pip install pytest.

Структура тестов: файлы test_*.py, функции test_*().

Практика:

Создайте папку week_1 → tests.

Напишите 3 теста для функций:

python
# tests/test_basics.py
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5

def test_add_negative():
    assert add(-1, -1) == -2

def test_add_floats():
    assert add(0.1, 0.2) == pytest.approx(0.3)
Коммит:

bash
git add tests/test_basics.py
git commit -m "feat: add basic pytest tests"
День 2 (27.04): Фикстуры
Теория:

Фикстуры (@pytest.fixture) для подготовки данных (например, тестовые пользователи).

Практика:

Создайте фикстуру для тестовых данных:

python
# tests/conftest.py
import pytest

@pytest.fixture
def user_data():
    return {"username": "test_user", "password": "qwerty123"}
Напишите тест, использующий фикстуру:

python
# tests/test_fixtures.py
def test_login(user_data):
    assert user_data["username"] == "test_user"
Коммит:

bash
git add tests/conftest.py tests/test_fixtures.py
git commit -m "feat: implement fixtures"
День 3 (28.04): Параметризация тестов
Теория:

Параметризация через @pytest.mark.parametrize.

Практика:

Напишите параметризованный тест для проверки умножения:

python
# tests/test_parametrization.py
import pytest

def multiply(a, b):
    return a * b

@pytest.mark.parametrize("a, b, expected", [
    (2, 3, 6),
    (-1, 5, -5),
    (0, 100, 0),
])
def test_multiply(a, b, expected):
    assert multiply(a, b) == expected
Коммит:

bash
git add tests/test_parametrization.py
git commit -m "feat: add parametrized tests"
День 4 (29.04): Обработка исключений
Теория:

Тестирование исключений с pytest.raises().

Практика:

Напишите тест для функции, которая вызывает ошибку:

python
# tests/test_exceptions.py
import pytest

def divide(a, b):
    if b == 0:
        raise ValueError("Cannot divide by zero!")
    return a / b

def test_divide_by_zero():
    with pytest.raises(ValueError):
        divide(10, 0)
Коммит:

bash
git add tests/test_exceptions.py
git commit -m "feat: exception handling tests"
День 5 (30.04): Генерация отчётов
Теория:

Установите pytest-html: pip install pytest-html.

Практика:

Запустите тесты с генерацией HTML-отчёта:

bash
pytest --html=report.html
Добавьте файл .gitignore (если его нет) и укажите в нём report.html.

Обновите GitHub Actions workflow, чтобы отчет генерировался автоматически:

yaml
# .github/workflows/pytest.yml
- name: Run tests
  run: pytest --html=report.html

- name: Upload report
  uses: actions/upload-artifact@v3
  with:
    name: pytest-report
    path: report.html
Коммит:

bash
git add .github/workflows/pytest.yml
git commit -m "docs: add pytest-html reports"
День 6 (01.05): Интеграция с GitHub Actions
Теория:

Как читать логи GitHub Actions.

Практика:

Запушьте изменения и проверьте вкладку Actions в GitHub.

Убедитесь, что отчет сохраняется как артефакт:


День 7 (02.05): Итоговый проект недели
Задача:

Напишите тесты для калькулятора с функциями: add, subtract, multiply, divide.

Используйте фикстуры, параметризацию и обработку исключений.

Сгенерируйте отчет и загрузите его в GitHub.

Пример структуры:

python
# tests/test_calculator.py
import pytest

class Calculator:
    def add(self, a, b):
        return a + b
    def subtract(self, a, b):
        return a - b
    # ... другие методы ...

@pytest.fixture
def calc():
    return Calculator()

@pytest.mark.parametrize("a, b, expected", [(5, 3, 2), (10, 1, 9)])
def test_subtract(calc, a, b, expected):
    assert calc.subtract(a, b) == expected
Коммит:

bash
git add tests/test_calculator.py
git commit -m "feat: final week 1 project"
