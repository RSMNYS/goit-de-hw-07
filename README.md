# Apache Airflow - Домашнє завдання 7

## Опис виконання завдання

Розроблено DAG, який виконує наступні завдання:

1. **Створює таблицю** в базі даних з полями id (автоінкремент, головний ключ), medal_type, count, created_at.
2. **Випадково обирає** одне із трьох значень: 'Bronze', 'Silver', 'Gold'.
3. **Розгалужує виконання** залежно від обраного значення.
4. **Підраховує кількість записів** у таблиці olympic_dataset.athlete_event_results для обраного типу медалі та записує результат у створену таблицю.
5. **Створює затримку** виконання на 35 секунд.
6. **Перевіряє свіжість запису** за допомогою сенсора, перевіряючи чи є записи, не старші за 30 секунд.
7. **Завершує виконання** DAG і відображає результати.

### Особливості реалізації

- Використано відокремлену функцію для створення операторів підрахунку медалей, що зменшує дублювання коду.
- DAG завершується успішно навіть якщо сенсор завершується з помилкою (завдяки оператору з `trigger_rule=ALL_DONE`).
- Сенсор перевірки свіжості запису цілеспрямовано "падає", оскільки затримка встановлена в 35 секунд, а сенсор шукає записи не старші за 30 секунд.
- Додано окремий оператор для перевірки результатів, який виводить дані з таблиці в логи Airflow.

### Результати виконання

- Після виконання DAG в таблиці `sergijr.hw_dag_results` з'являються записи з типами медалей та їх кількістю.
- Завдання перевірки свіжості запису (`check_record_freshness`) завершується з помилкою через затримку.
- Незважаючи на помилку сенсора, DAG в цілому завершує виконання і показує результати.

![Screenshot 2025-04-07 at 01.39.35.png](Screenshot%202025-04-07%20at%2001.39.35.png)

![Screenshot 2025-04-07 at 01.39.59.png](Screenshot%202025-04-07%20at%2001.39.59.png)
## Висновок

Розроблений DAG демонструє основні можливості Apache Airflow для роботи з базами даних, розгалуження виконання, використання сенсорів та управління потоком виконання завдань. Цей приклад показує, як можна налаштувати обробку помилок і забезпечити завершення DAG навіть у випадку невдалого виконання окремих завдань.
