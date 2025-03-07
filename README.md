# Завдання 1: Класи тварин
class Animal:
    def __init__(self, name: str, species: str):
        self.name = name
        self.species = species

    def make_sound(self):
        return "Some generic sound"

class Dog(Animal):
    def __init__(self, name: str, breed: str):
        super().__init__(name, "Dog")
        self.breed = breed

    def make_sound(self):
        return "Woof!"

class Cat(Animal):
    def __init__(self, name: str, color: str):
        super().__init__(name, "Cat")
        self.color = color

    def make_sound(self):
        return "Meow!"

# Завдання 2: Класи осіб
class Person:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def get_age(self):
        return self.age

class Driver(Person):
    def __init__(self, name: str, age: int, license_number: str):
        super().__init__(name, age)
        self.license_number = license_number

# Завдання 3: Класи транспортних засобів
class Vehicle:
    def __init__(self, speed: float):
        self.speed = speed

    def move(self):
        return f"Moving at {self.speed} km/h"

class Car(Vehicle):
    def __init__(self, speed: float, brand: str):
        super().__init__(speed)
        self.brand = brand

class Bicycle(Vehicle):
    def __init__(self, speed: float, type_: str):
        super().__init__(speed)
        self.type_ = type_

# Завдання 4: Класи пристроїв
class Device:
    def turn_on(self):
        return "Device is turned on"

    def turn_off(self):
        return "Device is turned off"

class Phone(Device):
    def __init__(self, model: str):
        self.model = model

class Laptop(Device):
    def __init__(self, brand: str):
        self.brand = brand

# Завдання 5: Класи мов програмування
class ProgrammingLanguage:
    def __init__(self, name: str):
        self.name = name

    def greet(self):
        return f"Hello from {self.name}!"

class Python(ProgrammingLanguage):
    def __init__(self):
        super().__init__("Python")

class JavaScript(ProgrammingLanguage):
    def __init__(self):
        super().__init__("JavaScrip
