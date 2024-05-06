# Задание 1

Для проверки монитора безопасности, необходимо изменить режим(mode = {"direction_1": "green", "direction_2": "green"}) на недопустимый (2 зеленых)

```python
...

class ControlSystem(Process):

    def __init__(self, monitor_queue: Queue):
        # вызываем конструктор базового класса
        super().__init__()
        # мы знаем только очередь монитора безопасности для взаимодействия с другими сущностями
        # прямая отправка сообщений в другую сущность запрещена в концепции FLASK
        self.monitor_queue = monitor_queue
        # создаём собственную очередь, в которую монитор сможет положить сообщения для этой сущности
        self._own_queue = Queue()

    # выдаёт собственную очередь для взаимодействия
    def entity_queue(self):
        return self._own_queue

    # основной код сущности
    def run(self):
        print(f'[{self.__class__.__name__}] старт')
        print(f'[{self.__class__.__name__}] отправляем тестовый запрос')

        mode = {"direction_1": "green", "direction_2": "green"}

        # запрос для сущности WorkerB - "скажи hello"

<SKIP>
    
```


### Результат работы
```bash
[монитор] старт
[ControlSystem] старт
[ControlSystem] отправляем тестовый запрос
[LightsGPIO] старт[ControlSystem] завершение работы

[монитор] обрабатываем событие Event(source='ControlSystem', destination='LightsGPIO', operation='set_mode', parameters='{"direction_1": "green", "direction_2": "green"}')
[монитор] проверяем конфигурацию {'direction_1': 'green', 'direction_2': 'green'}
[монитор] событие не разрешено политиками безопасности
```