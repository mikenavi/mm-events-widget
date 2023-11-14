# MM Widget

- [Конфигурация элемента](#конфигурация-элемента)
- [Конфигурация `operators`](#конфигурация-operators)
- [Конфигурация `offers`](#конфигурация-offers)
- [Пример `operators`](#пример-operators)
- [Пример `offers`](#пример-offers)

## Конфигурация элемента

```html
<div id="mm-widget" data-key="WIDGET_KEY" data-socket="SOCKET_URL"></div>
```

## Конфигурация `operators`

Содержит 2 ключа `operators` и `schedule`

### `operators` - Массив операторов

```json
{
  "key": "mikenavi",
  "image": "https://cdn.discordapp.com/avatars/724913702066847854/735dfbf52f898e89a3fb9c50f2eb4447.webp?size=32"
}
```

- `key` - идентификатор оператора
- `image` - url картинки-автара

### `schedule` - Массив смен

```json
{
  "days": [1, 3, 5, "2023-02-05", "2023-02-05"],
  "periods": [
    {
      "start": "00-00",
      "operators": ["mikenavi", "Miri"],
      "clients": [5, 15]
    },
    {
      "start": "09-00",
      "operators": ["mikenavi", "Miri"],
      "clients": [5, 15]
    },
    {
      "start": "15-00",
      "operators": ["mikenavi", "Miri"],
      "clients": [5, 15]
    },
    {
      "start": "20-00",
      "operators": ["mikenavi", "Miri"],
      "clients": [5, 15]
    },
    {
      "start": "13-00",
      "operators": ["Miri"],
      "clients": [1, 5]
    }
  ]
}
```

- `days` - массив дат или дней недели для которых составлено расписание.
  - Дата задаётся в **строковом** формате _"YYYY-MM-DD"_
  - День недели задаётся в **числовом** формате _N_ (в пределах от `1` до `7`, где `1` - это понедельник)
  - Повторное объявление дня или даты не допускается. При повторном объявлении одного и того же дня недели или или даты конфиг будет проигнорирован
  - Дата имеет больший приоритет над днём недели. Если конфиг содержит одновременно и дату и соответствующий дате день недели, то будет использован конфиг даты.
- `periods` - массив временных отсечек
  - `start` - время старта в формате _"HH-MM"_
  - `operators` - массив ключей активных операторов. Если задан пустой массив операторов, то в виджете выводится сообщение о том что операторов нет
  - `clients` - минимальное и максимальное число клиентов в смену, при необходимости указания фиксированного числа клиентов задаётся двумя одинаковыми значениями, например `[10, 10]`

## Конфигурация `offers`

### `products` - Массив продуктов слота виджета

```json
{
  "key": "product1",
  "image": "https://mmonster.co/media/94/f8/82/1669996120/1-mmnstr-raids-normal.jpg",
  "name": "Vault of the Incarnates Heroic Raid Boost",
  "link": "https://mmonster.co/products/Vault-of-the-Incarnates-Heroic-Raid-Boost",
  "badge": "Hot offer",
  "comment": "2 spots left"
}
```

- `key` - идентификатор продукта
- `image` - URL картинки продукта
- `name` - Название продукта
- `link` - Ссылка на продукт
- `badge` - Бедж
  - _опционально_
- `comment` - Комментарий, справа от беджа
  - _опционально_

### `schedule`

```json
{
  "days": [1, 3, 5, "2023-02-05", "2023-02-05"],
  "periods": [
    {
      "start": [
        "15-00",
        "15-15",
        "15-30",
        "15-45",
        "16-00",
        "16-15",
        "16-30",
        "16-45",
        "17-00"
      ],
      "key": "product1"
    },
    {
      "start": ["17-15", "17-30", "17-45"],
      "key": "product2",
      "badge": "Hot offer"
    },
    {
      "start": ["18-00", "18-15"],
      "key": "product1",
      "comment": "1 spot left"
    }
  ]
}
```

- `days` - массив дат или дней недели для которых составлено расписание.
  - Дата задаётся в **строковом** формате _"YYYY-MM-DD"_
  - День недели задаётся в **числовом** формате _N_ (в пределах от `1` до `7`, где `1` - это понедельник)
  - Повторное объявление дня или даты не допускается. При повторном объявлении одного и того же дня недели или или даты конфиг будет проигнорирован
  - Дата имеет больший приоритет над днём недели. Если конфиг содержит одновременно и дату и соответствующий дате день недели, то будет использован конфиг даты.
- `periods` - массив временных отсечек
  - `start` - массив строк времени старта в формате _"HH-MM"_
    - Если время старта не объявлено, то таймер в виджете будет отсутствовать
    - Товар без объявленного времени имеет меньший приоритет перед товарами с объявленным временем
  - `key` - ключ продукта
  - `image` - URL картинки продукта
    - _опционально, имеет более высокий приоритет над продуктом_
  - `name` - Название продукта
    - _опционально, имеет более высокий приоритет над продуктом_
  - `link` - Ссылка на продукт
    - _опционально, имеет более высокий приоритет над продуктом_
  - `badge` - Бедж
    - _опционально, имеет более высокий приоритет над продуктом_
  - `comment` - Комментарий, справа от беджа
    - _опционально, имеет более высокий приоритет над продуктом_

### Пример `operators`

```json
{
  "operators": [
    {
      "key": "mikenavi",
      "image": "https://cdn.discordapp.com/avatars/724913702066847854/735dfbf52f898e89a3fb9c50f2eb4447.webp?size=32"
    },
    {
      "key": "Miri",
      "image": "https://cdn.discordapp.com/avatars/200645209716031489/b1d94e3950c174a1fc2c1f03f11a6943.webp?size=32"
    },
    {
      "key": "Jexon",
      "image": "https://cdn.discordapp.com/avatars/222796809993453570/fd874922ef01fe6c5cb391aebde3cd21.webp?size=32"
    }
  ],
  "schedule": [
    {
      "days": [1, 3, 5],
      "periods": [
        {
          "start": "00-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "09-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "15-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "20-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "13-00",
          "operators": ["Miri"],
          "clients": [1, 5]
        }
      ]
    },
    {
      "days": [2, 4, 6],
      "periods": [
        {
          "start": "00-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "09-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "15-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "20-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "13-00",
          "operators": ["Miri"],
          "clients": [1, 5]
        }
      ]
    },
    {
      "days": [7],
      "periods": [
        {
          "start": "00-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "09-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "15-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "20-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "13-00",
          "operators": ["Miri"],
          "clients": [1, 5]
        }
      ]
    },
    {
      "days": ["2023-02-06"],
      "periods": [
        {
          "start": "00-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "09-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "15-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "20-00",
          "operators": ["mikenavi", "Miri"],
          "clients": [5, 15]
        },
        {
          "start": "13-00",
          "operators": ["Miri"],
          "clients": [1, 5]
        }
      ]
    }
  ]
}
```

### Пример `offers`

```json
{
  "products": [
    {
      "key": "product1",
      "image": "https://mmonster.co/media/94/f8/82/1669996120/1-mmnstr-raids-normal.jpg",
      "name": "Vault of the Incarnates Heroic Raid Boost",
      "link": "https://mmonster.co/products/Vault-of-the-Incarnates-Heroic-Raid-Boost",
      "badge": "Hot offer",
      "comment": "2 spots left"
    },
    {
      "key": "product2",
      "image": "https://mmonster.co/media/ae/1f/5d/1669659011/1-mmnstr-gear.jpg",
      "name": "Dragonflight PvE Gear Boost",
      "link": "https://mmonster.co/products/Dragonflight-PvE-Gear-Boost",
      "badge": "Hot offer"
    },
    {
      "key": "product3",
      "image": "https://mmonster.co/media/70/51/b6/1671564220/1-mmnstr-raids-easy.jpg",
      "name": "Vault of the Incarnates Normal Raid Boost",
      "link": "https://mmonster.co/products/Vault-of-the-Incarnates-Normal-Raid-Boost",
      "badge": "Hot offer"
    },
    {
      "key": "product4",
      "image": "https://mmonster.co/media/62/1a/f6/1671309322/3-mmnstr-dungeons-hardest.jpg",
      "name": "Mythic+ Dungeons Combo Pack",
      "link": "https://mmonster.co/products/Mythic-Dungeons-Combo-Pack"
    }
  ],
  "schedule": [
    {
      "days": [1, 3, 5],
      "periods": [
        {
          "start": [
            "15-00",
            "15-15",
            "15-30",
            "15-45",
            "16-00",
            "16-15",
            "16-30",
            "16-45",
            "17-00"
          ],
          "key": "product1"
        },
        {
          "start": ["17-15", "17-30", "17-45"],
          "key": "product2",
          "badge": "Hot offer"
        },
        {
          "start": ["18-00", "18-15"],
          "key": "product1",
          "comment": "1 spot left"
        }
      ]
    },
    {
      "days": [2, 4, 6],
      "periods": [
        {
          "start": [
            "15-00",
            "15-15",
            "15-30",
            "15-40",
            "16-00",
            "16-15",
            "16-30",
            "16-45",
            "17-00"
          ],
          "key": "product1"
        },
        {
          "start": ["17-15", "17-30", "17-45"],
          "key": "product2",
          "badge": "Hot offer"
        },
        {
          "start": ["18-00", "18-15"],
          "key": "product1",
          "comment": "1 spot left"
        }
      ]
    },
    {
      "days": [7],
      "periods": [
        {
          "start": [
            "15-00",
            "15-20",
            "15-30",
            "15-48",
            "16-00",
            "16-15",
            "16-30",
            "16-45",
            "17-00",
            "19-15"
          ],
          "key": "product4"
        },
        {
          "start": ["14-30", "17-15", "17-30", "17-45"],
          "key": "product2",
          "badge": "Hot offer"
        },
        {
          "start": ["18-00", "18-15"],
          "key": "product1",
          "comment": "1 spot left"
        }
      ]
    },
    {
      "days": ["2023-02-06"],
      "periods": [
        {
          "start": ["14-45"],
          "key": "product4"
        },
        {
          "start": [
            "15-00",
            "15-15",
            "15-30",
            "15-45",
            "16-00",
            "16-15",
            "16-30",
            "16-45",
            "17-00"
          ],
          "key": "product1"
        },
        {
          "start": ["17-15", "17-30", "17-45"],
          "key": "product2",
          "badge": "Hot offer"
        },
        {
          "start": ["18-15"],
          "key": "product1",
          "comment": "1 spot left"
        }
      ]
    }
  ]
}
```
