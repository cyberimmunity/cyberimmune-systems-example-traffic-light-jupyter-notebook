# Задание 2

1. Добавляем новый режим "мигающий желтый"
```python
from multiprocessing import Queue, Process
from multiprocessing.queues import Empty
import json

# формат управляющих команд для монитора
@dataclass
class ControlEvent:
    operation: str

# список разрешенных сочетаний сигналов светофора
# любые сочетания, отсутствующие в этом списке, запрещены
traffic_lights_allowed_configurations = [
    {"direction_1": "red", "direction_2": "green"},
    {"direction_1": "red", "direction_2": "red"},    
    {"direction_1": "red", "direction_2": "yellow"},    
    {"direction_1": "yellow", "direction_2": "yellow"},    
    {"direction_1": "off", "direction_2": "off"},
    {"direction_1": "green", "direction_2": "red"},    
    {"direction_1": "green", "direction_2": "yellow"},
    {"direction_1": "yellow_blinking", "direction_2": "yellow_blinking"},
]

```

2. Изменяем конфигурацию
```python
def run(self):        
        print(f'[{self.__class__.__name__}] старт')
        print(f'[{self.__class__.__name__}] отправляем тестовый запрос')

        mode = {"direction_1": "yellow_blinking", "direction_2": "yellow_blinking"}
```

## Результаты работы
```bash
[монитор] старт
[ControlSystem] старт
[ControlSystem] отправляем тестовый запрос
[LightsGPIO] старт[ControlSystem] завершение работы

[монитор] обрабатываем событие Event(source='ControlSystem', destination='LightsGPIO', operation='set_mode', parameters='{"direction_1": "yellow_blinking", "direction_2": "yellow_blinking"}')
[монитор] проверяем конфигурацию {'direction_1': 'yellow_blinking', 'direction_2': 'yellow_blinking'}
[монитор] отправляем запрос Event(source='ControlSystem', destination='LightsGPIO', operation='set_mode', parameters='{"direction_1": "yellow_blinking", "direction_2": "yellow_blinking"}')
[LightsGPIO] ControlSystem запрашивает изменение режима {"direction_1": "yellow_blinking", "direction_2": "yellow_blinking"}
[LightsGPIO] новый режим: {"direction_1": "yellow_blinking", "direction_2": "yellow_blinking"}!
[LightsGPIO] завершение работы
```