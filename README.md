import random

class Cat:
    def __init__(self, name):
        self.name = name

    def play(self):
        return f"{self.name} the cat is playing."

    def sleep(self):
        return f"{self.name} the cat is sleeping."

class Dog:
    def __init__(self, name):
        self.name = name

    def play(self):
        return f"{self.name} the dog is playing."

    def sleep(self):
        return f"{self.name} the dog is sleeping."

class Student:
    def __init__(self, name):
        self.name = name
        self.money = 100
        self.knowledge = 0
        self.stress = 0
        self.cat = Cat("Whiskers")
        self.dog = Dog("Buddy")

    def work(self):
        self.money += 50
        self.stress += 10
        return f"{self.name} worked and earned $50."

    def study(self):
        self.knowledge += 10
        self.stress += 5
        return f"{self.name} studied and gained knowledge."

    def relax(self):
        self.stress -= 20
        return f"{self.name} is relaxing."

    def spend_money(self):
        self.money -= 20
        return f"{self.name} spent $20 on holiday."

    def live_day(self):
        if self.money < 20:
            return self.work()
        elif self.stress > 50:
            return self.relax()
        elif self.knowledge < 50:
            return self.study()
        else:
            return self.spend_money()

    def live_year(self):
        events = []
        for day in range(365):
            event = self.live_day()
            events.append(event)
            if random.random() < 0.3:
                events.append(self.cat.play())
            if random.random() < 0.3:
                events.append(self.dog.play())
            if random.random() < 0.1:
                events.append(self.cat.sleep())
            if random.random() < 0.1:
                events.append(self.dog.sleep())
        return events

# Simulate a student's life for a year
student = Student("John")
events = student.live_year()

# Print the events of the year
for event in events:
    print(event)
