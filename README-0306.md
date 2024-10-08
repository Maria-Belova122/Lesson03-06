# Задание по теме "Подробнее о функциях"

data_structure = [
    [1, 2, 3],
    {'a': 4, 'b': 5},
    (6, {'cube': 7, 'drum': 8}),
    "Hello",
    ((), [{(2, 'Urban', ('Urban2', 35))}])
]


def calculate_structure_sum(data_structure):
    # sum_ – переменная для суммы всех чисел и длин всех строк списка
    # sum_ – результат выполнения функции (return sum_)
    sum_ = 0
    if len(data_structure) > 0:
        # Если список не пуст проверяем каждый элемент списка, если пуст – ничего не делаем
        for i in range(len(data_structure)):
            argm = data_structure[i]
            # Проверяем каждый элемент списка на тип данных
            if isinstance(argm, str):  # Строка
                # Добавим к сумме sum_ длину строки
                sum_ += len(argm)
            elif isinstance(argm, bool):  # Логич.значение True или False
                # Преобразуем логическое значение в строку
                # Добавим к сумме sum_ длину строки str(argm)
                sum_ += len(str(argm))
            elif isinstance(argm, set) or isinstance(argm, tuple):  # Множество или кортеж
                # Преобразуем множество или кортеж в список list(argm) и
                # Увеличим сумму на результат функции для нового списка
                sum_ += calculate_structure_sum(list(argm))
            elif isinstance(argm, list):  # Список
                # Увеличим сумму на результат функции для списка
                sum_ += calculate_structure_sum(argm)
            elif isinstance(argm, dict):  # Словарь
                if len(argm) > 0:
                    list_keys = argm.keys()
                    list_values = argm.values()
                    # Составим список list_dict из всех ключей и значений словаря
                    list_dict = list(list_keys) + list(list_values)
                    # Увеличиваем сумму на результат функции для списка list_dict
                    sum_ += calculate_structure_sum(list_dict)
                else:  # Пустой словарь {}
                    continue
            # Из всех типов данных остались только числа (int и float)
            # Добавим число к сумме sum_
            else:
                sum_ += argm

    return sum_


result = calculate_structure_sum(data_structure)
print(data_structure, ' - список')
print(result, ' - сумма всех чисел и длин всех строк списка')