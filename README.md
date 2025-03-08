import colorama
import inspect

# Отримуємо список атрибутів модуля
attributes = dir(colorama)

# Виводимо ключові атрибути та їхні типи
for attr in attributes:
    print(f"{attr}: {type(getattr(colorama, attr))}")

# Дослідимо вміст модуля colorama
print("\nДоступні методи та класи в colorama:\n")
for name, obj in inspect.getmembers(colorama):
    if inspect.isclass(obj) or inspect.ismodule(obj) or inspect.isfunction(obj):
        print(f"{name}: {obj}")


from colorama import Fore, Back, Style, init

init(autoreset=True)  # Автоматично скидає стиль після кожного виклику

print(Fore.RED + "Цей текст червоний")
print(Back.YELLOW + "Цей текст на жовтому фоні")
print(Style.BRIGHT + "Цей текст яскравий")
print(Fore.GREEN + Back.BLACK + "Зелений текст на чорному фоні")

git init
git add colorama_introspection.py
git commit -m "Дослідження бібліотеки colorama"
git branch -M main
git remote add origin https://github.com/USERNAME/REPOSITORY.git
git push -u origin main
