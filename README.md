# Неблагоприятные метеорологические условия

Неблагоприятные метеорологические условия (НМУ) – метеорологические (погодные) условия,
способствующие накоплению вредных (загрязняющих) веществ в приземном слое атмосферного воздуха.

В репозитории размещены данные о НМУ, собранные из официальных открытых источников, в формате `JSON`.

## Визуализация имеющихся данных

Для оценки объемов и качества данных из различных источников
на [странице проекта](https://gradocus.github.io/adverse-weather-conditions/#visualization)
размещены интерактивные графики.

## Описание структуры файлов

Структура источников данных (`/data/sources.json`):

```
{
    "atime": "2017-11-19T07:30:27Z",
    "cities": [{
        "name": {
            "en": "Chelyabinsk",
            "ru": "Челябинск"
        },
        "path": "chelyabinsk"
    }],
    "name": {
        "en": "City administration of Chelyabinsk",
        "ru": "Администрация города Челябинска"
    },
    "url": {
        "domain": "cheladmin.ru",
        "root": {
            "en": "https://cheladmin.ru/en",
            "ru": "https://cheladmin.ru/ru"
        }
    }
}
```

Каждый источник содержит время последнего обращения (`atime`), список городов (`cities`), название (`name`)
и информацию об адресе источника (`url.domain` используется только для получения пути к файлу данных сообщений о НМУ).

Структура сообщений о НМУ (`/data/{ source.url.domain }/{ city.path }.json`):

```
{
    "daterange": [
        "2015-05-26T19:00:00+05:00",
        "2015-05-27T19:00:00+05:00"
    ],
    "level": 1,
    "path": "soobshcheniya-o-nmu"
}
```

Как правило, источники содержат информацию о НМУ в следующем виде:

> ... с 19.00 часов 26.05.2015 до 19.00 часов 27.05.2015 ожидаются НМУ 1 степени опасности ...

Период действия предупреждения о НМУ (`daterange`) приведен к формату ISO 8601 с указание местного часового пояса
(`YYYY-MM-DDThh:mm:ss±hh:mm`). Параметр `path` используется для формирования ссылки непосредственно на источник информации:
`{ source.url.root.ru }/{ path }`.
