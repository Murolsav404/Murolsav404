from typing import List

# Завдання 1: Керування завданнями
class Task:
    def __init__(self, title: str, description: str, deadline: str):
        self.title = title
        self.description = description
        self.deadline = deadline
        self.completed = False

    def mark_completed(self):
        self.completed = True

class TaskManager:
    def __init__(self):
        self.tasks: List[Task] = []

    def add_task(self, task: Task):
        self.tasks.append(task)

    def remove_task(self, title: str):
        self.tasks = [task for task in self.tasks if task.title != title]

    def show_tasks(self):
        for task in self.tasks:
            status = "✔ Done" if task.completed else "❌ Not done"
            print(f"{task.title} - {task.deadline} [{status}]")

# Завдання 2: Онлайн-магазин
class Product:
    def __init__(self, name: str, price: float, stock: int):
        self.name = name
        self.price = price
        self.stock = stock

class Cart:
    def __init__(self):
        self.items: List[Product] = []

    def add_product(self, product: Product):
        if product.stock > 0:
            self.items.append(product)
            product.stock -= 1

    def remove_product(self, product_name: str):
        self.items = [item for item in self.items if item.name != product_name]

    def total_price(self):
        return sum(item.price for item in self.items)

# Завдання 3: Банківська система
class BankAccount:
    def __init__(self, owner: str, account_number: str, balance: float = 0):
        self.owner = owner
        self.account_number = account_number
        self.balance = balance

    def deposit(self, amount: float):
        self.balance += amount

    def withdraw(self, amount: float):
        if amount <= self.balance:
            self.balance -= amount

    def transfer(self, amount: float, recipient_account: 'BankAccount'):
        if amount <= self.balance:
            self.balance -= amount
            recipient_account.balance += amount

class Bank:
    def __init__(self):
        self.accounts: List[BankAccount] = []

    def add_account(self, account: BankAccount):
        self.accounts.append(account)

# Завдання 4: Керування персоналом
class Employee:
    def __init__(self, name: str, position: str, salary: float):
        self.name = name
        self.position = position
        self.salary = salary

class Department:
    def __init__(self, name: str):
        self.name = name
        self.employees: List[Employee] = []

    def add_employee(self, employee: Employee):
        self.employees.append(employee)

    def remove_employee(self, name: str):
        self.employees = [emp for emp in self.employees if emp.name != name]

    def total_salary(self):
        return sum(emp.salary for emp in self.employees)

student = Student("John")
events = student.live_year()

# Print the events of the year
for event in events:
    print(event)
