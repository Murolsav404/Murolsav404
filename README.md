from colorama import Fore, Back, Style, init

init(autoreset=True)  # Автоматично скидає стиль після кожного виклику

print(Fore.RED + "Цей текст червоний")
print(Back.YELLOW + "Цей текст на жовтому фоні")
print(Style.BRIGHT + "Цей текст яскравий")
print(Fore.GREEN + Back.BLACK + "Зелений текст на чорному фоні")
