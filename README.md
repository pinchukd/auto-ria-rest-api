# Тенденции на рынке б/у авто с REST API AUTO.RIA
**Отслеживайте, анализируйте и прогнозируйте**

Мы запускаем в свободное пользование **“Подсчёт средней цены”** — 
первый сервис, основанный на актуальных статистических данных **AUTO.RIA** (ежемесячно 10 тыс. опубликованных объявлений о продаже 7 800 марок авто, которые ежедневно собирают 8 млн. просмотров).

Теперь вы можете:
* узнавать актуальные средние цены автомобилей разных марок и моделей; 
* следить за изменениями цен в кратко- и долгосрочном периодах;
* анализировать и прогнозировать изменения цен и спроса на автомобили;
* размещать полученную информацию на вашем сайте.`*`

```
* Наличие ссылки на сайт AUTO.RIA с гиперссылкой на страницу http://AUTO.RIA.com, 
не закрытой для индексации поисковыми системами, является единственным 
обязательным требованием для использования сервиса.
```

Ознакомьтесь с технической документацией, чтобы получить доступ и экспортировать необходимую информацию в программу вашей компании.

Благодарим за содействие в запуске сервиса “Подсчёт средней цены” ТОВ «Богдан–Авто Холдинг».

Ваш AUTO.RIA, автосайт № 1 в Украине.


# REST API сайта AUTO.RIA.com

API возвращает данные в формате JSON. Формат данных в большинстве случаев стандартный - коллекция объектов с полями *name* (название объекта) и *value* (его идентификатор).

Идентификатор любой сущности является целым числом.

## Содержание

- [Подсчет средней цены](#user-content-Подсчет-средней-цены)
   + [Список поддерживаемых параметров](#user-content-Список-поддерживаемых-параметров)
   + [Формат данных в запросе](#user-content-Формат-данных-в-запросе)
   + [Формат данных в ответе](#user-content-Формат-данных-в-ответе)
   + [Примеры](#user-content-Примеры)
- [Методы для работы с типами транспорта и кузова](#user-content-Методы-для-работы-с-типами-транспорта-и-кузова)
   + [Типы транспорта](#user-content-Типы-транспорта)
   + [Типы кузова](#user-content-Типы-кузова)
- [Методы для работы с марками и моделями](#user-content-Методы-для-работы-с-марками-и-моделями)
   + [Марки](#user-content-Марки)
   + [Модели](#user-content-Модели)
- [Методы для работы с областями и городами](#user-content-Методы-для-работы-с-областями-и-городами)
   + [Области](#user-content-Области)
   + [Города](#user-content-Города)
- [Методы для работы с техническими характеристиками](#user-content-Методы-для-работы-с-техническими-характеристиками)
   + [Коробки передач](#user-content-Коробки-передач)
   + [Типы привода](#user-content-Типы-привода)
   + [Типы топлива](#user-content-Типы-топлива)
   + [Опции](#user-content-Опции)
- [Цвета](#user-content-Цвета)
- [Растаможка](#user-content-Растаможка)
- [После ДТП](#user-content-После-ДТП)
- [Взято в кредит](#user-content-Взято-в-кредит)
- [Конфискат](#user-content-Конфискат)
- [Не на ходу](#user-content-Не-на-ходу)

## Подсчет средней цены

### Список поддерживаемых параметров

На данный момент поддерживаются следующие параметры:

|  Название           | Параметр в строке запроса | Тип данных   |
|:--------------------|:--------------------------|:------------:|
|  [Тип транспорта](#user-content-Типы-транспорта)  |    main_category   | `Number`    |
|  [Тип кузова](#user-content-Типы-кузова)         |  body_id                  |  `Number`      |
|  [Марка](#user-content-Марки)              |  marka_id                 |  `Number`      |
|  [Модель](#user-content-Модели)             |  model_id                 |  `Number`      |
|  Год выпуска        |  yers                     |  `Number[]`  |
|  [Коробка передач](#user-content-Коробки-передач)    |  gear_id                  |  `Number[]`      |
|  [Тип топлива](#user-content-Типы-топлива)        |  fuel_id                  |  `Number`      |
|  [Тип привода](#user-content-Типы-топлива)        |  drive_id                 |  `Number`      |
|  Объем двигателя    |  engineVolume             |  `Number`      |
|  [Опции](#user-content-Опции)              |  options                  |  `Number[]`      |
|  Пробег             |  raceInt                  |  `Number[]`  |
|  Количество дверей  |  door                     |  `Number`      |
|  [Область](#user-content-Области)            |  state_id                 |  `Number`      |
|  [Город](#user-content-Города)              |  city_id                  |  `Number`      |
|  Грузоподъемность   |  carrying                 |  `Number`      |
|  Количество мест    |  seats                    |  `Number`      |
|  [Цвет](#user-content-Цвета)               |  color_id                 |  `Number`      |
|  [Растаможка](#user-content-Растаможка)         |  custom               | `Number`         |
|  [После ДТП](#user-content-После-ДТП) | damage | `Number`|
|  [Взято в кредит](#user-content-Взято-в-кредит) | under_credit | `Number` |
|  [Конфискат](#user-content-Конфискат) | confiscated_car | `Number` |
|  [Не на ходу](#user-content-Не-на-ходу) |onRepairParts |`Number`|

### Формат данных в запросе

Все параметры описанные в таблице поддерживаемых параметров должны передаватся в виде чисел. Исключениями являются только параметры - *год выпуска*. *пробег*, *опции* и *коробка передач*.

Если передать массив в параметре *коробка передач*, то это будет интерпретироваться как поиск коробок передач с логическим оператором *ИЛИ*. Т.е. `http://api.auto.ria.com/average?marka_id=9&model_id=31612&gear_id=1&gear_id=2` - выберет для подсчета все **BMW 318** с автоматическими и ручными коробками передач.

Если передать массив в параметре *год выпуска* или *пробег* это будет интерпретироваться как диапазон значений. Например, `http://api.auto.ria.com/average?raceInt=10&raceInt=100` - выберет для подсчета средней цены все объявления с пробегом от 10 до 100 тыс. км.

Если передать массив значений в параметре *опции* это будет интерпретироваться как поиск опций с логическим оператором "И". Т.е. `http://api.auto.ria.com/average?options=217&options=463` выберет для подсчета все объявления, у которых есть опция *ABS* **И** *Галогенные фары*.

### Формат данных в ответе

В случае успешного подсчета средней цены по указанным параметрам результат будет со статусом **200 OK**.

Пример успешного ответа:
```javascript
{
    total: 17,
    arithmeticMean: 16305.882352941177,
    interQuartileMean: 8483.333333333334,
    percentiles: {
        1.0: 1944,
        5.0: 2520,
        25.0: 3500,
        50.0: 8000,
        75.0: 23500,
        95.0: 53539.999999999985,
        99.0: 64868
    },
    prices: [
        67700,
        27000,
        3000,
        23500,
        3500,
        8100,
        10000,
        3500,
        2700,
        8000,
        11000,
        45800,
        50000,
        1800,
        4350,
        4400,
        2850
    ],
    classifieds: [
        14663610,
        14226353,
        14138132,
        13969588,
        14697569,
        13386778,
        13279188,
        14555863,
        14754932,
        14816842,
        14664706,
        13873344,
        14681607,
        14772056,
        14059841,
        14290096,
        14890250
    ]
}
```
Расшифровка параметров:
- *total* - общее количество объявлений, учавствующих в подсчете.
- *arithmeticMean* - [среднее арифметическое](https://ru.wikipedia.org/wiki/%D0%A1%D1%80%D0%B5%D0%B4%D0%BD%D0%B5%D0%B5_%D0%B0%D1%80%D0%B8%D1%84%D0%BC%D0%B5%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%BE%D0%B5).
- *interQuartileMean* - среднее арифметическое из значений, находящихся между первым и четвертым [квантилем](https://ru.wikipedia.org/wiki/%D0%9A%D0%B2%D0%B0%D0%BD%D1%82%D0%B8%D0%BB%D1%8C). Грубо говоря, это среднее арифметическое без учета 25% самых маленьких и самых больших значений.
- *percentiles* - значения [процентилей](https://ru.wikipedia.org/wiki/%D0%9A%D0%B2%D0%B0%D0%BD%D1%82%D0%B8%D0%BB%D1%8C#.D0.9F.D0.B5.D1.80.D1.86.D0.B5.D0.BD.D1.82.D0.B8.D0.BB.D1.8C). Т.е. для данного примера 25% всех объявлений имеют цену ниже $3500.
- *prices* - список цен, которые учавствовали в подсчете средней цены. Размер ограничен 1000 элементов.
- *classifieds* - идентификаторы объявлений, к которым принадлежат цены соответственно. Размер ограничен 1000 элементов.

Если по каким-либо причинам не удалось подсчитать среднюю цену, ответ будет иметь статус **400 Bad Request**, а тело ответа будет содержать следующее:
```javascript
{ "message": "Not Enough Data" }
```

### Примеры

Средняя цена по BMW X5 с пробегом от 10 до 100 тыс. км. - [http://api.auto.ria.com/average?marka_id=9&model_id=96&raceInt=10&raceInt=100](http://api.auto.ria.com/average?marka_id=9&model_id=96&raceInt=10&raceInt=100).


Средняя цена для Honda Accord в Киеве - [http://api.auto.ria.com/average?marka_id=28&model_id=262&city_id=9](http://api.auto.ria.com/average?marka_id=28&model_id=262&city_id=9)

## Методы для работы с типами транспорта и кузова

### Типы транспорта

Получить список типов транспорта можно отправив GET запрос на адрес [http://api.auto.ria.com/categories](http://api.auto.ria.com/categories). Результат будет примерно следующим:
```javascript
[
    { name: "Легковые", value: 1 },
    { name: "Мото", value: 2 },
    { name: "Водный транспорт", value: 3 },
    { name: "Спецтехника", value: 4 },
    { name: "Прицеп", value: 5 },
    { name: "Грузовик", value: 6 },
    { name: "Автобус", value: 7 },
    { name: "Автодом", value: 8 },
    { name: "Воздушный транспорт", value: 9 }
]
```

### Типы кузова

Типы кузова зависят от типов транспорта. Поэтому для того, чтобы получить список типов кузова необходимо отправить GET запрос на адрес `http://api.auto.ria.com/categories/:categoryId/bodystyles`, где *categoryId* - идентификатор типа транспорта.

Например, для легковых автомобилей ([http://api.auto.ria.com/categories/1/bodystyles](http://api.auto.ria.com/categories/1/bodystyles)), результат будет следующим:
```javascript
[
    { name: "Седан", value: 3 },
    { name: "Внедорожник / Кроссовер", value: 5 },
    { name: "Минивэн", value: 8 },
    { name: "Хэтчбек", value: 4 },
    { name: "Универсал", value: 2 },
    { name: "Купе", value: 6 },
    { name: "Легковой фургон (до 1,5 т)", value: 254 },
    { name: "Кабриолет", value: 7 },
    { name: "Пикап", value: 9 },
    { name: "Лимузин", value: 252 },
    { name: "Другой", value: 28 }
]
```

Также типы кузова могут быть разделены на группы. Это актуально для спецтехники. Поэтому существует способ получить сгруппированные типы кузова отправив GET запрос по адресу `http://api.auto.ria.com/categories/:categoryId/bodystyles/_group`, где *categoryId* - идентификатор типа транспорта.

Например, для мотоциклов ([http://api.auto.ria.com/categories/2/bodystyles/_group](http://api.auto.ria.com/categories/2/bodystyles/_group)), результат будет следующим:
```javascript
[
    [
        { name: "Мопеды", value: 58 },
        { name: "Скутер / Мотороллер", value: 11 },
        { name: "Макси-скутер", value: 12 }
    ],
    [
        { name: "Мотоциклы", value: 13 },
        { name: "Мотоцикл Без обтекателей (Naked bike)", value: 15 },
        { name: "Мотоцикл Внедорожный (Enduro)", value: 21 },
        { name: "Мотоцикл Кастом", value: 30 },
        { name: "Мотоцикл Классик", value: 14 },
        { name: "Мотоцикл Кросс", value: 19 },
        { name: "Мотоцикл Круизер", value: 24 },
        { name: "Мотоцикл Многоцелевой (All-round)", value: 25 },
        { name: "Мотоцикл с коляской", value: 29 },
        { name: "Спортбайк", value: 18 },
        { name: "Мотоцикл Спорт-туризм", value: 17 },
        { name: "Мотоцикл Супермото (Motard)", value: 22 },
        { name: "Мотоцикл Триал", value: 20 },
        { name: "Мотоцикл Туризм", value: 16 },
        { name: "Мотоцикл Чоппер", value: 23 }
    ],
    [
        { name: "Мини мотоциклы", value: 31 },
        { name: "Мини спорт", value: 32 },
        { name: "Мини крос (Питбайк)", value: 33 }
    ],
        { name: "Трицикл", value: 34 },
        { name: "Трайк", value: 57 },
    [
        { name: "Квадроциклы", value: 35 },
        { name: "Квадроцикл детский", value: 36 },
        { name: "Квадроцикл спортивный", value: 39 },
        { name: "Квадроцикл утилитарный", value: 41 },
        { name: "Мотовездеход", value: 42 },
        { name: "Вездеход-амфибия", value: 43 },
        { name: "Гольф-кар", value: 44 },
        { name: "Картинг", value: 45 }
    ],
    { name: "Снегоход", value: 46 },
    { name: "Другое", value: 56 }
]
```

Формат данных при этом отличается от обычного - это коллекция объектов, в которой есть другие коллекции. Группа типов кузовов всегда начинается с её названия. Например, в группу *Квадроциклы* входят типы кузовов *Квадроцикл детский*, *Квадроцикл спортивный*, *Квадроцикл утилитарный*, *Мотовездеход* и т.д.

Также, при необходимости, можно получиться просто весь список типов кузовов, послав GET запрос по адресу [http://api.auto.ria.com/bodystyles](http://api.auto.ria.com/bodystyles).

## Методы для работы с марками и моделями

### Марки

Марки зависят от типов транспорта. Поэтому для того, чтобы получить список марок необходимо отправить GET запрос по адресу `http://api.auto.ria.com/categories/:categoryId/marks`, где *categoryId* - идентификатор типа транспорта.

Например, для легковых автомобилей ([http://api.auto.ria.com/categories/1/marks](http://api.auto.ria.com/categories/1/marks)), результат будет следующим:
```javascript
[
    { name: "Acura", value: 98 },
    { name: "Adler", value: 2396 },
    { name: "Aixam", value: 2 },
    { name: "Alfa Romeo", value: 3 },
    { name: "Alpine", value: 100 },
    { name: "Altamarea", value: 3988 },
    { name: "Aro", value: 101 },
    { name: "Artega", value: 3105 },
    { name: "Asia", value: 4 },
    { name: "Aston Martin", value: 5 },
    { name: "Audi", value: 6 },
    { name: "Austin", value: 7 },
    { name: "Autobianchi", value: 102 }
    ...
]
```

### Модели

Модели зависят от типов транспорта и марок. Следовательно список марок можно получить по адресу `http://api.auto.ria.com/categories/:categoryId/marks/:markId/models`, где *categoryId* - идентификатор типа транспорта а *markId* - идентификатор марки.

Например, для мотоциклов BMW ([http://api.auto.ria.com/categories/2/marks/9/models](http://api.auto.ria.com/categories/2/marks/9/models)), список моделей будет следующим:
```javascript
[
    { name: "Adventure", value: 25290 },
    { name: "C", value: 25291 },
    { name: "CS", value: 25292 },
    { name: "DKW", value: 28318 },
    { name: "F", value: 25293 },
    { name: "G", value: 29468 },
    { name: "GS", value: 25295 },
    { name: "HP", value: 38148 },
    { name: "Independent", value: 25297 },
    { name: "K", value: 25298 },
    { name: "LT", value: 25299 },
    { name: "R", value: 25300 },
    { name: "RS", value: 32736 },
    { name: "RT", value: 25301 },
    { name: "S", value: 25302 },
    { name: "X", value: 42030 }
]
```

Модели, также как и типы кузовов, могут быть сгруппированы. Чтобы получить такой список, необходимо отправить запрос по адресу `http://api.auto.ria.com/categories/:categoryId/marks/:markId/models/_group`, где *categoryId* - идентификатор типа транспорта а *markId* - идентификатор марки.

Например, для легковых автомобилей BMW ([http://api.auto.ria.com/categories/1/marks/9/models/_group](http://api.auto.ria.com/categories/1/marks/9/models/_group)), список моделей будет следующим:
```javascript
[
    [
        { name: "1 Series (все)", value: 2161 },
        { name: "116", value: 34670 },
        { name: "118", value: 34671 },
        { name: "120", value: 34672 },
        { name: "123", value: 34673 },
        { name: "125", value: 34674 },
        { name: "130", value: 34675 },
        { name: "135", value: 34676 }
    ],
    [
        { name: "3 Series (все)", value: 3219 },
        { name: "3 Series GT", value: 43029 },
        { name: "315", value: 37454 },
        { name: "316", value: 30851 },
        { name: "318", value: 31612 },
        { name: "320", value: 31611 },
        { name: "321", value: 37389 },
        { name: "323", value: 34677 },
        { name: "324", value: 30687 },
        { name: "325", value: 29713 },
        { name: "326", value: 44061 },
        { name: "328", value: 31661 },
        { name: "330", value: 34678 },
        { name: "335", value: 34679 },
        { name: "340", value: 35568 }
    ],
    ...
    { name: "Alpina", value: 906 },
    { name: "Dixi", value: 33383 },
    { name: "I3", value: 44838 },
    { name: "I8", value: 44537 },
    { name: "Isetta", value: 32380 },
    { name: "Z1", value: 97 },
    { name: "Z3", value: 98 },
    { name: "Z4", value: 99 },
    { name: "Z8", value: 100 }
]
```
Формат данных такой же как и в случае с типа кузова - коллекция объектов, в которой могут быть другие объекты. Группа моделей всегда начинается с её названия.

Также, при необходимости, можно просто получить список всех моделей, отправив GET запрос по адресу [http://api.auto.ria.com/models](http://api.auto.ria.com/models).

## Методы для работы с областями и городами

### Области

Получить список областей можно отправив GET запрос по адресу [http://api.auto.ria.com/states](http://api.auto.ria.com/states).

Результат будет следующим:
```javascript
[
    { name: "Винницкая", value: 1 },
    { name: "Волынская", value: 18 },
    { name: "Днепропетровская", value: 11 },
    { name: "Донецкая", value: 13 },
    { name: "Житомирская", value: 2 },
    { name: "Закарпатская", value: 22 },
    { name: "Запорожская", value: 14 },
    { name: "Ивано-Франковская", value: 15 },
    { name: "Киевская", value: 10 },
    { name: "Кировоградская", value: 16 },
    { name: "Луганская", value: 17 },
    { name: "Львовская", value: 5 },
    { name: "Николаевская", value: 19 },
    { name: "Одесская", value: 12 },
    { name: "Полтавская", value: 20 },
    { name: "Республика Крым", value: 21 },
    { name: "Ровенская", value: 9 },
    { name: "Сумская", value: 8 },
    { name: "Тернопольская", value: 3 },
    { name: "Харьковская", value: 7 },
    { name: "Херсонская", value: 23 },
    { name: "Хмельницкая", value: 4 },
    { name: "Черкасская", value: 24 },
    { name: "Черниговская", value: 6 },
    { name: "Черновицкая", value: 25 }
]
```

### Города

Города зависят от областей, поэтому, чтобы получить их список, необходимо послать GET запрос по адресу `http://api.auto.ria.com/states/:stateId/cities`, где *stateId* - идентификатор области.

Например, для Винницкой области ([http://api.auto.ria.com/states/1/cities](http://api.auto.ria.com/states/1/cities)) список городов будет следующим:
```javascript
[
    { name: "Винница", value: 1 },
    { name: "Жмеринка", value: 27 },
    { name: "Казатин", value: 30 },
    { name: "Крыжополь", value: 31 },
    { name: "Липовец", value: 32 },
    { name: "Литин", value: 33 },
    { name: "Могилев-Подольский", value: 34 },
    { name: "Мурованые Куриловцы", value: 35 },
    { name: "Немиров", value: 36 },
    { name: "Оратов", value: 37 },
    { name: "Песчанка", value: 38 },
    { name: "Погребище", value: 39 },
    { name: "Теплик", value: 40 },
    { name: "Тывров", value: 41 },
    { name: "Томашполь", value: 42 },
    { name: "Тростянец", value: 43 },
    { name: "Тульчин", value: 44 },
    { name: "Хмельник", value: 45 },
    { name: "Черновцы", value: 46 },
    { name: "Чечельник", value: 47 },
    { name: "Шаргород", value: 48 },
    { name: "Ямполь", value: 49 },
    { name: "Бар", value: 597 },
    { name: "Бершадь", value: 599 },
    { name: "Гайсин", value: 602 },
    { name: "Ильинцы", value: 603 },
    { name: "Калиновка", value: 604 },
    { name: "Гнивань", value: 609 },
    { name: "Ладыжин", value: 644 }
]
```

## Методы для работы с техническими характеристиками

### Коробки передач

Коробки передач зависят от типа транспорта, поэтому, чтобы получить их список, необходимо послать GET запрос по адресу `http://api.auto.ria.com/categories/:categoryId/gearboxes`, где *categoryId* - идентификатор типа транспорта.

Например, список коробок передач для мотоциклов ([http://api.auto.ria.com/categories/2/gearboxes](http://api.auto.ria.com/categories/2/gearboxes)) будет выглядеть следующим образом:
```javascript
[
    { name: "Ручная / Механика", value: 1 },
    { name: "Автомат", value: 2 },
    { name: "Типтроник", value: 3 },
    { name: "Адаптивная", value: 4 },
    { name: "Вариатор", value: 5 }
]
```

### Типы привода

Типы привода также зависят от типа транспорта, поэтому, чтобы получить их список, необходимо плсать GET запрос по адресу `http://api.auto.ria.com/categories/:categoryId/driverTypes`, где *categoryId* - идентификатор типа транспорта.

Например, список типов привода для мотоциклов ([http://api.auto.ria.com/categories/2/driverTypes](http://api.auto.ria.com/categories/2/driverTypes)) выглядит следующим образом:
```javascript
[
    { name: "Кардан", value: 4 },
    { name: "Ремень", value: 5 },
    { name: "Цепь", value: 6 }
]
```

### Типы топлива

Типы топлива можно получить отправив GET запрос по адресу [http://api.auto.ria.com/fuels](http://api.auto.ria.com/fuels). Ответ будет выглядеть так:
```javascript
[
    { name: "Бензин", value: 1 },
    { name: "Дизель", value: 2 },
    { name: "Газ", value: 3 },
    { name: "Газ/бензин", value: 4 },
    { name: "Гибрид", value: 5 },
    { name: "Электро", value: 6 },
    { name: "Другое", value: 7 },
    { name: "Газ метан", value: 8 },
    { name: "Газ пропан-бутан", value: 9 }
]
```

### Опции

Опции зависят от типа транспорта. Получить их список можно отправив GET запрос по адресу `http://api.auto.ria.com/categories/:categoryId/options`, где *categoryId* - идентификатор типа транспорта.

Например, список опций для легковых автомобилей ([http://api.auto.ria.com/categories/1/options](http://api.auto.ria.com/categories/1/options)) будет выглядеть примерно так:
```javascript
[
    { name: "ABD", value: 354 },
    { name: "ABS", value: 217 },
    { name: "ESP", value: 459 },
    { name: "Галогенные фары", value: 463 },
    { name: "Замок на КПП", value: 481 },
    { name: "Иммобилайзер", value: 225 },
    { name: "Пневмоподвеска", value: 442 },
    { name: "Подушка безопасности (Airbag)", value: 211 },
    { name: "Серворуль", value: 485 },
    { name: "Сигнализация", value: 303 },
    ...
]
```

## Цвета

Получить список всех цветов можно, если отправить GET запрос по адресу [http://api.auto.ria.com/colors](http://api.auto.ria.com/colors). Результат будет седующим:
```javascript
[
    { name: "Бежевый", value: 1 },
    { name: "Черный", value: 2 },
    { name: "Синий", value: 3 },
    { name: "Бронзовый", value: 4 },
    { name: "Коричневый", value: 5 },
    { name: "Золотой", value: 6 },
    { name: "Зеленый", value: 7 },
    { name: "Серый", value: 8 },
    { name: "Апельсин", value: 9 },
    { name: "Магнолии", value: 10 },
    { name: "Розовый", value: 11 },
    { name: "Фиолетовый", value: 12 },
    { name: "Красный", value: 13 },
    { name: "Серебряный", value: 14 },
    { name: "Белый", value: 15 },
    { name: "Желтый", value: 16 },
    { name: "Голубой", value: 17 },
    { name: "Вишнёвый", value: 18 },
    { name: "Сафари", value: 19 },
    { name: "Гранатовый", value: 20 },
    { name: "Асфальт", value: 21 }
]
```

## Растаможка ##

Параметр растаможки может принимать только два значения: `1` - нерастаможенный и `0` - растаможенный.


## После ДТП ##

Данный параметр принимает следующие значения:
`1` - объявления после ДТП
`0` - остальные объявления

## Взято в кредит ##

Данный параметр может принимать следующие значения:
`1` - объявления взятые в кредит
`0` - остальные объявления

## Конфискат ##

Данный параметр может принимать следующие значения:
`1` - только конфискованные объявления
`0` - только неконфискованные объявления

## Не на ходу ##

Данный параметр может принимать следующие значения:
`1` - только объявления не на ходу
`0` - только объявления на ходу


##Получение информации об автомобиле

Запрос:

https://auto.ria.com/blocks_search_ajax/view/auto/15923375/?lang_id=2

Ответ:

{
  "current_timestamp": 1440489663.493,
  "additional_params": {
    "lang_id": 2,
    "view_type_id": 0,
    "user_id": null
  },
  "result": {
    "statistic_data": {
      "views": 0
    },
    "relinked_description": "",
    "is_auto_added_by_partner": false,
    "auto_data": {
      "auto_id": 15923375,
      "marka_id": 55,
      "model_id": 2197,
      "version": "1.2T AT SE+ (Navi)",
      "body_id": 5,
      "door": 5,
      "gear_id": 5,
      "color_id": 13,
      "metallic": 1,
      "fuel_id": 1,
      "yers": 2015,
      "engineVolume": 1.2,
      "race": {
        "race": 0,
        "raceInt": 0
      },
      "raceInt": 0,
      "description": "* 25 800  живыми деньгами!   NEW! 2015!  В НАЛИЧИИ! Камера заднего вида с 7-дюймовым цветным сенсорным дисплеем+НАВИГАЦИОННАЯ СИСТЕМА;ABS;(NCC)-КОМПЛЕКС СИСТЕМ УПРАВЛЕНИЯ ШАССИ;(ESP)-Электроная система динамичической стабилизации;(EBD)-Электроная система распределения тормозных усилий на каждое колесо отдельно;(ATC)-СИСТЕМА АКТИВНОГО КОНТРОЛЯ ТРАЕКТОРИИ;(TCS)-Электроная противобуксовочная система;(NBA)-Электроный усилитель экстренного торможения;(AEB)-СИСТЕМА АКТИВНОГО ТОРМОЖЕНИЯ ДВИГАТЕЛЕМ;(HSA)-Система помощи при старте вгору; Датчики:Дождя+ Освещенности+Внешней температуры; ЭЛЕКТРИЧЕСКИЙ ОБОГРЕВ ЛОБОВОГО СТЕКЛА;Электро-усилитель руля с изменяемым усилием+двухрежимная система-NORMAL и SPORT;ЦЗ с ДУ+иммобилайзер;AM/FM/CD/MP3 магнитола+6-динамиков с Bluetooth(телефон)+аудиовходAUX+входUSB-устройств и iPod/iPhone+система объемного звучания-управление системой на руле(свободные руки);Бортовой компьютер с большим многофункциональным ЖК-дисплеем-управление с руля;КЛИРЕНС=200мм",
      "price": 609400,
      "currency_id": 3,
      "auctionPossible": 1,
      "onRepairParts": 0,
      "priceMain": 0,
      "user_id": 1027429,
      "add_date": "2015-08-19T06:08:56.000Z",
      "update_date": "2015-08-21T11:13:29.000Z",
      "status_id": 0,
      "expiried_date": "2015-08-25T07:01:03.000Z",
      "partner_id": 1,
      "ip": 3287182758,
      "with_photo": 71,
      "state_id": 4,
      "city_id": 4,
      "saled_date": "0000-00-00 00:00:00",
      "is_new": 0,
      "damage": 0,
      "custom": 0,
      "main_photo_id": 134842664,
      "group_id": 0,
      "is_exchange": 1,
      "exchangeTypeId": 0,
      "page_rank": 0,
      "top20": 0,
      "top20_regional": 0,
      "send_comments": 0,
      "under_credit": 0,
      "with_video": 0,
      "dont_comment": 0,
      "category_id": "1",
      "main_category": 1,
      "drive_id": 2,
      "VIN": "SJNFEAJ11U1307576",
      "xml_import_id": 0,
      "is_hot": 0,
      "fishki": 0,
      "power": 115,
      "power_name": 1,
      "confiscated_car": 0,
      "vip": 0,
      "checked_auto_ria": 0,
      "matched_country": 826,
      "country_ip": "xx",
      "can_be_checked": 0,
      "seats": 5,
      "carrying": 0,
      "from_archive": 0,
      "years": 2015,
      "color_data": {
        "lang_id": 2,
        "color_id": 13,
        "name": "Красный",
        "eng": "red",
        "genitive": "Красного",
        "dative": "Красному",
        "accusative": "Красный",
        "ablative": "Красным",
        "locative": "Красном",
        "adjective": "Красный",
        "adjective_female": "Красная",
        "adjective_plural": "Красные",
        "metallic": 1
      },
      "drive_data": {
        "drive_id": 2,
        "name": "Передний"
      },
      "body_category": {
        "sub_cat_id": 5,
        "name": "Внедорожник / Кроссовер",
        "body_rewrite": "vnedorozhnik-krossover"
      },
      "gearbox_data": {
        "lang_id": 2,
        "gearbox_id": 5,
        "name": "Вариатор",
        "eng": "variator",
        "slang": "вариатор,коробка вариатор",
        "slang_ablative": "вариатором,коробкой вариатором"
      },
      "auto_test": 0,
      "marka_data": {
        "slang": "Ниссан",
        "lang_id": 2,
        "marka_id": 55,
        "name": "Nissan",
        "set_cat": "1,3,4,5,6,7",
        "main_category": 1,
        "active": 1,
        "country_id": 392,
        "eng": "nissan",
        "count": 6039,
        "fit": 0,
        "rewrite": "nissan"
      },
      "model_data": {
        "slang": "Кашкай",
        "lang_id": 2,
        "model_id": 2197,
        "marka_id": 55,
        "name": "Qashqai",
        "set_cat": "1",
        "active": 1,
        "is_group": 0,
        "parent_id": 0,
        "eng": "qashqai",
        "count": 390,
        "fit": 0,
        "rewrite": "qashqai"
      },
      "exchange": {
        "is_exchange": 1,
        "exchangeTypeId": 0,
        "exchangeTypes": [
          "Любой",
          "Моя доплата",
          "Ваша доплата",
          "Равноценный"
        ]
      },
      "fuel_data": {
        "fuel_id": 1,
        "name": "Бензин",
        "eng": "benzin",
        "rates": [],
        "smallTitle": ".",
        "title": "Город: не указано, Трасса: не указано, Смешанный: не указано"
      }
    },
    "description": "* 25 800  живыми деньгами!   NEW! 2015!  В НАЛИЧИИ! Камера заднего вида с 7-дюймовым цветным сенсорным дисплеем+НАВИГАЦИОННАЯ СИСТЕМА;ABS;(NCC)-КОМПЛЕКС СИСТЕМ УПРАВЛЕНИЯ ШАССИ;(ESP)-Электроная система динамичической стабилизации;(EBD)-Электроная система распределения тормозных усилий на каждое колесо отдельно;(ATC)-СИСТЕМА АКТИВНОГО КОНТРОЛЯ ТРАЕКТОРИИ;(TCS)-Электроная противобуксовочная система;(NBA)-Электроный усилитель экстренного торможения;(AEB)-СИСТЕМА АКТИВНОГО ТОРМОЖЕНИЯ ДВИГАТЕЛЕМ;(HSA)-Система помощи при старте вгору; Датчики:Дождя+ Освещенности+Внешней температуры; ЭЛЕКТРИЧЕСКИЙ ОБОГРЕВ ЛОБОВОГО СТЕКЛА;Электро-усилитель руля с изменяемым усилием+двухрежимная система-NORMAL и SPORT;ЦЗ с ДУ+иммобилайзер;AM/FM/CD/MP3 магнитола+6-динамиков с Bluetooth(телефон)+аудиовходAUX+входUSB-устройств и iPod/iPhone+система объемного звучания-управление системой на руле(свободные руки);Бортовой компьютер с большим многофункциональным ЖК-дисплеем-управление с руля;КЛИРЕНС=200мм",
    "from_archive": 0,
    "saled_ok": 0,
    "VIN": "SJNFEAJ11U1307576",
    "partner_id": 1,
    "auto_archive_data": {
      "status": 0
    },
    "other_data": {
      "zapchasti_link": "http://zapchasti.ria.com/nissan/qashqai/?utm_source=auto&utm_medium=link_zapchasti&utm_campaign=obyava",
      "is_hot": 0,
      "super": 0,
      "can_be_checked": 0,
      "exchangeTypeId": 0,
      "fishki": 0,
      "with_video": 0,
      "page_rank": 0,
      "top20": 0,
      "top20_regional": 0,
      "send_comments": 0,
      "dont_comment": 0,
      "is_bold": 0
    },
    "user_phones": [
      {
        "phone_id": "674945377",
        "user_id": "1027429",
        "phone": "0673140438",
        "region_code_size": "3",
        "checked": "1",
        "is_mobile": "1",
        "prio": "0",
        "country_code": "38",
        "phone_code": "067",
        "phone_number": "3140438",
        "phone_formatted": "(067) 314-04-38",
        "additional_data": {
          "phone_id": "674945377",
          "call_from": "08:00",
          "call_till": "24:00",
          "call_name": "Павел"
        }
      },
      {
        "phone_id": "674945384",
        "user_id": "1027429",
        "phone": "0673140435",
        "region_code_size": "3",
        "checked": "1",
        "is_mobile": "1",
        "prio": "0",
        "country_code": "38",
        "phone_code": "067",
        "phone_number": "3140435",
        "phone_formatted": "(067) 314-04-35",
        "additional_data": {
          "phone_id": "674945384",
          "call_from": "08:00",
          "call_till": "24:00",
          "call_name": "Александр"
        }
      },
      {
        "phone_id": "674945386",
        "user_id": "1027429",
        "phone": "0673802027",
        "region_code_size": "3",
        "checked": "1",
        "is_mobile": "1",
        "prio": "0",
        "country_code": "38",
        "phone_code": "067",
        "phone_number": "3802027",
        "phone_formatted": "(067) 380-20-27",
        "additional_data": {
          "phone_id": "674945386",
          "call_from": "08:00",
          "call_till": "24:00",
          "call_name": "Денис"
        }
      },
      {
        "phone_id": "674945402",
        "user_id": "1027429",
        "phone": "0673140436",
        "region_code_size": "3",
        "checked": "1",
        "is_mobile": "1",
        "prio": "0",
        "country_code": "38",
        "phone_code": "067",
        "phone_number": "3140436",
        "phone_formatted": "(067) 314-04-36",
        "additional_data": {
          "phone_id": "674945402",
          "call_from": "",
          "call_till": "",
          "call_name": "ПРОДАЖ Б/У авто Сергей"
        }
      }
    ],
    "matched_country": {
      "id": 826,
      "name": "Англия",
      "eng": "united-kingdom"
    },
    "power_data": {
      "power": {
        "1": {
          "rate": 115,
          "name": "л.с."
        },
        "2": {
          "rate": 84.64,
          "name": "кВт"
        }
      },
      "main": 1
    },
    "category_data": {
      "category_id": 1,
      "main_category": 1,
      "category_name": "Легковые",
      "category_path": "legkovie"
    },
    "user_data": {
      "user_id": "1027429",
      "ip": 3287182758,
      "registration_date": "2010-09-07 10:39:22",
      "city_id": "4",
      "state_id": "4",
      "firstName": "Сергей",
      "lastName": "",
      "hide_ads_status": 0,
      "hide_registration": 0,
      "contact_via_email": 1,
      "isAutoseller": true,
      "show_converted_price": 1,
      "postalAddres": "ул.Свободы,15/1А",
      "show_page": 0
    },
    "location_data": {
      "state_id": 4,
      "state": {
        "lang_id": 2,
        "stateID": 4,
        "name": "Хмельницкая",
        "eng_name": "khmelnickij",
        "declension": "Хмельницкой области",
        "center_declension": "Хмельницкого",
        "region_name": "Хмельницкий",
        "eng": "khmelnickij"
      },
      "city": {
        "lang_id": 2,
        "cityID": 4,
        "stateID": 4,
        "name": "Хмельницкий",
        "eng": "khmelnickij",
        "declension": "Хмельницкий"
      }
    },
    "company_data": [],
    "photo_data": {
      "count": 71,
      "photos_count": 71,
      "photo": {
        "photo_id": 134842664,
        "auto_id": 15923375,
        "status": 0,
        "checked": 1,
        "standard": 0,
        "date_add": "2015-07-21 10:48:12",
        "description": null,
        "url": "auto/photo/13484/1348426/134842664/134842664.jpg",
        "image": "auto/photo/13484/1348426/134842664/134842664.jpg",
        "little": 1,
        "resize": 1,
        "ftp": 1,
        "ftp_count": 0,
        "flag": 0,
        "is_main": 0,
        "checksum": "",
        "size": 0,
        "is_video": 0,
        "original_lose": 0,
        "seo_link": "auto/photo/nissan_qashqai__134842664.jpg"
      },
      "photos": [
        {
          "seo_link": "auto/photo/nissan_qashqai__134842494.jpg",
          "photo_id": 134842494
        },
        {
          "seo_link": "auto/photo/nissan_qashqai__134842639.jpg",
          "photo_id": 134842639
        },
        {
          "seo_link": "auto/photo/nissan_qashqai__134842642.jpg",
          "photo_id": 134842642
        },
        {
          "seo_link": "auto/photo/nissan_qashqai__134842648.jpg",
          "photo_id": 134842648
        },
        {
          "seo_link": "auto/photo/nissan_qashqai__134842649.jpg",
          "photo_id": 134842649
        },
        {
          "seo_link": "auto/photo/nissan_qashqai__134842654.jpg",
          "photo_id": 134842654
        },
        {
          "seo_link": "auto/photo/nissan_qashqai__134842655.jpg",
          "photo_id": 134842655
        },
        {
          "seo_link": "auto/photo/nissan_qashqai__134842658.jpg",
          "photo_id": 134842658
        }
      ]
    },
    "date_data": {
      "current_timestamp": 1440489663,
      "add": "2015-08-19 09:08:56",
      "add_timestamp": 1439964536,
      "expiried": "2015-08-25 10:01:03",
      "expiried_timestamp": 1440486063,
      "update": "2015-08-21 14:13:29",
      "saled": "0000-00-00 00:00:00",
      "date_add": {
        "year": "2010",
        "short_year": "10",
        "month": "09",
        "full_month": "09",
        "day": "07",
        "hours": "10",
        "minutes": "39",
        "seconds": "22",
        "year_differential": 71068
      },
      "publication_expiried_date": "2015-11-19 09:08:56",
      "publication_expiried_timestamp": 1447916936,
      "publication_status_id": 2
    },
    "autosalon_data": {
      "autosalon_id": 551,
      "user_id": 1027429,
      "name": "Nissan  Лига-II",
      "geo_X": 26.998573299497,
      "geo_Y": 49.432076861941,
      "geo_Zoom": 150,
      "website": "http://www.liga-nissan.km.ua",
      "announce": "<p style=\"text-align: justify;\"><strong>С 19.04.2006 Автоцентр &laquo;ЛИГА-II&raquo; является авторизированным официальным дилером <a href=\"http://www.liga-nissan.km.ua/nissan-models-3.html\">Nissan</a> в Украине, расположенный в городе Хмельницкий.</strong></p>\r\n<p style=\"text-align: justify;\"><a href=\"http://www.liga-nissan.km.ua\">Автоцентр &laquo;ЛИГА-ІІ&raquo;</a> &mdash; это концептуальный <strong>3S</strong> комплекс (<strong>S</strong>ale  &mdash; салон, <strong>S</strong>ervice &mdash; сервис,<strong> S</strong>pareparts &mdash; запчасти), который соответствует всем высоким корпоративным стандартам Nissan.</p>\r\n<p style=\"text-align: justify;\">C 2008 года <a href=\"http://www.liga-nissan.km.ua  \">Автоцентр &laquo;ЛИГА-ІІ&raquo;</a> также является авторизированным официальным сервис-дилером Infiniti в Украине.<br />\r\n<a href=\"http://www.liga-nissan.km.ua  \">Автоцентр &laquo;ЛИГА-ІІ&raquo;</a> осуществляет продажу новых автомобилей <a href=\"http://www.liga-nissan.km.ua/nissan-models-3.html\">Nissan</a>, гарантийное и послегарантийное обслуживание автомобилей <a href=\"http://www.liga-nissan.km.ua/nissan-models-3.html\">Nissan</a> и Infiniti, покрасочные и кузовные работы, продажу оригинальных запасных частей и аксессуаров к автомобилям <a href=\"http://www.liga-nissan.km.ua/nissan-models-3.html\">Nissan</a> и Infiniti.<br />\r\nДополнительно дилерский центр предлагает своим клиентам услуги по оформлению кредита, страхованию автомобиля и регистрации в МРЕО ГАИ. На территории центра есть большой паркинг, уютный кафе-бар, комфортная зона отдыха и ожидания.</p>",
      "logo": "auto/new_autosalon/0/5/551/551.jpg",
      "created_at": "2011-06-25T08:42:14.000Z",
      "description": "<p style=\"text-align: center;\"><img src=\"http://img.ria.ua/photos/auto/text_photos/0/23/2354/2354.jpg\" alt=\"\" /></p>\r\n<p>&nbsp;</p>",
      "exlusive_marka": 0,
      "comments_disabled": 0,
      "show_old_count": 1,
      "exlusive_state": 0,
      "paket_id": 1,
      "is_test_drive": 0,
      "active": 1,
      "updated_at": "2015-08-02T22:30:14.000Z",
      "manager_id": 0,
      "date_closed": "2016-02-15T22:00:00.000Z",
      "payment_item_id": 35886508,
      "start_shipping": "2015-08-18T21:00:00.000Z",
      "price": 4560,
      "work_time_mon_fr": "[\"09:00\",\"19:00\",\"1\",\"5\"]",
      "work_time_sat": "[\"09:00\",\"17:00\",\"6\"]",
      "work_time_sun": "[\"10:00\",\"15:00\",\"7\"]",
      "state_id": 4,
      "city_id": 4,
      "company_type": 1,
      "address": "ул.Свободы,15/1А",
      "cityID": 4,
      "stateID": 4,
      "cityName": "Хмельницкий",
      "packageName": "Старт",
      "salon_activ": 1,
      "enable": 0,
      "outer_url": "http://www.liga-nissan.km.ua"
    },
    "price_data": {
      "currency_id": 3,
      "main_price": 609400,
      "prices_curr_rate": {
        "1": 0.04526,
        "2": 0.04012,
        "3": 1
      },
      "currencies": {
        "1": {
          "id": 1,
          "name": "USD",
          "position": 0,
          "denotation": "$"
        },
        "2": {
          "id": 2,
          "name": "EUR",
          "position": 0,
          "denotation": "&euro;"
        },
        "3": {
          "id": 3,
          "name": "UAH",
          "position": 1,
          "denotation": "грн."
        }
      },
      "prices": {
        "1": 27581.444,
        "2": 24449.128,
        "3": 609400
      },
      "oldCurrencies": 3,
      "oldPrices": {
        "1": 0,
        "2": 0,
        "3": 0
      }
    },
    "img_data": {},
    "levelData": {
      "level": 216,
      "expire": "2015-08-26T06:08:57.000Z",
      "hotType": 1
    }
  },
  "black_list": 0
}

