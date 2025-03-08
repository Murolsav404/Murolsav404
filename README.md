# Завдання 1: Створення ітерованого об'єкта
class IterableObject:
    def __init__(self, data):
        self.data = data
    
    def __iter__(self):
        return (item for item in self.data)

# Перевірка
iter_obj = IterableObject([1, 2, 3, 4, 5])
for item in iter_obj:
    print(item)

# Завдання 2: Декоратор для калькулятора
import operator

def calculator_decorator(func):
    def wrapper(expression):
        allowed_operators = {'+': operator.add, '-': operator.sub, '*': operator.mul, '/': operator.truediv}
        try:
            tokens = expression.split()
            if len(tokens) != 3:
                raise ValueError("Формат виразу повинен бути: число оператор число")
            
            num1, op, num2 = tokens
            num1, num2 = float(num1), float(num2)
            
            if op not in allowed_operators:
                raise ValueError(f"Оператор '{op}' не підтримується")
            
            result = allowed_operators[op](num1, num2)
            return result
        except Exception as e:
            return f"Помилка: {e}"
    return wrapper

@calculator_decorator
def calculate(expression):
    return eval(expression)  # eval більше не використовується напряму

# Перевірка
print(calculate("10 + 5"))  # 15.0
print(calculate("10 / 0"))  # Помилка: ділення на нуль
print(calculate("10 & 5"))  # Помилка: оператор не підтримується

# Додаткове завдання: Ітерований студент
class StudentSimulator:
    def __init__(self, name, days):
        self.name = name
        self.days = days
        self.current_day = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.current_day >= len(self.days):
            raise StopIteration
        day_result = f"День {self.current_day + 1}: {self.days[self.current_day]}"
        self.current_day += 1
        return day_result

# Перевірка
student = StudentSimulator("Іван", ["Відвідав лекцію", "Написав тест", "Здав домашку"])
for day in student:
    print(day)
