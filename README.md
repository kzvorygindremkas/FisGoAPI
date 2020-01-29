# FisGo API

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

# Описание API внешних чеков платформы FisGo
Внешний чек "external_purchase" - чек для фискализации, поступающий через Poll API

##### Структура чека 
```json
{
  "data": {
    "type": "",
    "taxMode": "",
    "positions": [],
    "payments": [],
    "attributes": {},
    "total": {},
    "tags": []
  }
}
```
#### Описание полей
    Ниже приведены массивы, структуры и поля, участвующие в парсе внешнего чека.
    Обязательность, точные наименования и формат полей представлена в API Кабинета Дримкас.
    [ARRAY]     массив
    [STRUCT]    структура полей
    [STRING]    текстовое поле
    [INT]       целочисленное поле
    
    [R]         (required) обязательное поле
>  
    ["type"]                        [STRING]    [R]     [Тип чека]
        ["SALE"]                                        [приход]
        ["REFUND"]                                      [возврат прихода]
        ["OUTFLOW"]                                     [расход]
        ["OUTFLOW_REFUND"]                              [возврат расхода]
>
    ["taxMode"]                     [STRING]            [Система налогообложения (СНО)]
        ["DEFAULT"]                                     [общая]
        ["SIMPLE"]                                      [упрощенная доход]
        ["SIMPLE_WO"]                                   [упрощенная доход минус расход]
        ["ENVD"]                                        [единый налог на вменённый доход]
        ["AGRICULT"]                                    [единый сельскохозяйственный налог]
        ["PATENT"]                                      [патентная система налогообложения]
>
    ["positions"]                   [ARRAY]     [R]     [Список позиций чека]
>
        ["rem_id"]                  [STRING]            [ID товара в кабинете]
>
        ["name"]                    [STRING]    [R]     [Наименование предмета расчета]
>
        ["type"]                    [STRING]    [R]     [Тип товара]>
            ["COUNTABLE"]                               [Штучный]
            ["SCALABLE"]                                [Весовой]
            ["SHOES"]                                   [Обувь]
            ["SERVICE"]                                 [Услуга]
>
        ["tags"]                    [ARRAY]             [Список тэгов ФФД (позиция)]
            [1171]                  [STRING]            [телефон поставщика]
            [1225]                  [STRING]            [наименование поставщика]
            [1226]                  [STRING]            [ИНН поставщика]
            [1229]                  [INT]               [акциз]
            [1230]                  [STRING]            [код страны товара]
            [1231]                  [STRING]            [код таможенной декларации]
            [1057]                  [INT]               [признак агента]
            [1044]                  [STRING]            [операция платёжного агента]
            [1005]                  [STRING]            [адрес оператора перевода]
            [1016]                  [STRING]            [ИНН оператора перевода]
            [1075]                  [STRING]            [телефон оператора перевода]
            [1073]                  [STRING]            [телефон платёжного агента]
            [1026]                  [STRING]            [наименование оператора перевода]
            [1074]                  [STRING]            [телефон оператора по приёму платежей]
            [1162]                  [STRING]            [код товара]
            [1191]                  [STRING]            [дополнительный реквизит предмета расчёта]
            [1214]                  [INT]               [признак способа расчёта]
            [1212]                  [INT]               [признак предмета расчёта]
            [1030]                  [STRING]            [наименование предмета расчёта]
            [777]                   [INT]               [сумма предоплаты на позицию
                                                        *системный тег, не содержится в ФФД]
>
        ["quantity"]                [INT]       [R]     [Количество предмета расчета]
>
        ["price"]                   [INT]       [R]     [Цена за еденицу расчета в копейках]
>
        ["total"]                   [INT]               [Стоимость предмета расчета в копейках]
>
        ["tax"]                     [STRING]            [НДС за еденицу предмета расчета]
            ["NDS_NO_TAX"]                              [Без НДС]
            ["NDS_0"]                                   [НДС 0%]
            ["NDS_10"]                                  [НДС 10%]
            ["NDS_20"]                                  [НДС 20%]
            ["NDS_10_CALCULATED"]                       [НДС Расчетная 10%]
            ["NDS_20_CALCULATED"]                       [НДС Расчетная 20%]
>
        ["tax_sum"]                 [INT]               [Сумма НДС за предмет расчета ]
>
    ["payments"]                    [ARRAY]     [R]     [Список платежей 
                                                        (*поддерживается только один вид платежа на чек)]
>
        ["sum"]                     [INT]       [R]     [Оплата в копейках]
>
        ["type"]                    [STRING]            [Тип оплаты]
            ["CASH"]                                    [Наличный расчет]
            ["CASHLESS"]                                [Безналичный расчет]
            ["PREPAID"]                                 [Аванс]
            ["CREDIT"]                                  [Кредит]
            ["CONSIDERATION"]                           [Встречное предоставление]
>
    ["attributes"]                  [STRUCT]            [Данные покупателя]
        ["phone"]                   [STRING]            [Телефонный номер. Шаблон - +\d{11}]
        ["email"]                   [STRING]            [Электронная почта. Шаблон - .+@..+]
>
    ["total"]                       [STRUCT]    [R]     [Итог чека]
>
        ["total_sum"]               [INT]       [R]     [итоговая сумма в копейках]
>
        ["taxes_sum"]               [STRING]            [Сумма примененных НДС в копейках, 
                                                        сгруппированных по типу]
            ["NDS_10"]                                  [НДС 10%]
            ["NDS_18"]                                  [НДС 20%]
            ["NDS_10_CALCULATED"]                       [НДС Расчетная 10%]
            ["NDS_20_CALCULATED"]                       [НДС Расчетная 20%]
>
    ["tags"]                        [ARRAY]             [Список тэгов ФФД (чек)]
        [1171]                      [STRING]            [телефон поставщика]
        [1225]                      [STRING]            [наименование поставщика]
        [1226]                      [STRING]            [ИНН поставщика]
        [1057]                      [INT]               [признак агента]
        [1044]                      [STRING]            [операция платёжного агента]
        [1005]                      [STRING]            [адрес оператора перевода]
        [1016]                      [STRING]            [ИНН оператора перевода]
        [1075]                      [STRING]            [телефон оператора перевода]
        [1073]                      [STRING]            [телефон платёжного агента]
        [1026]                      [STRING]            [наименование оператора перевода]
        [1074]                      [STRING]            [телефон оператора по приёму платежей]
        [1227]                      [STRING]            [покупатель]
        [1228]                      [STRING]            [ИНН покупателя]
        [1085]                      [STRING]            [наименование дополнительного реквизита пользователя]
        [1086]                      [STRING]            [значение дополнительного реквизита пользователя]
        [1192]                      [STRING]            [дополнительный реквизит чека (БСО)]
        [1215]                      [INT]               [сумма по чеку (БСО) предоплатой 
                                                        (зачётом аванса и (или) предыдущих платежей)]

#### Примеры
---
> Тип операции: приход
> Тип оплаты: безналичными
> Данные покупателя содержат тел. номер и email покупателя
> Тип товара: штучный
> Тип НДС: без НДС
> CНО: Общая
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX"
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Тип операции: расход
> Тип оплаты: наличными
> Данные покупателя содержат тел. номер
> Тип товара: весовой
> Тип НДС: НДС 10%
> CНО: Упрощённая доход
```json
{
  "type": "OUTFLOW",
  "payments": [
    {
      "type": "CASH",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Весовой товар",
      "quantity": 2000,
      "price": 100,
      "type": "SCALABLE",
      "tax": "NDS_10"
    }
  ],
  "taxMode": "SIMPLE"
}
```
---
> Тип операции: возврат прихода
> Тип оплаты: аванс
> Данные покупателя содержат email покупателя
> Тип товара: обувь
> Тип НДС: НДС 0%
> CНО: Упрощенная доход минус расход
```json
{
  "type": "REFUND",
  "payments": [
    {
      "type": "PREPAID",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Обувь",
      "quantity": 2,
      "price": 100,
      "type": "SHOES",
      "tax": "NDS_0"
    }
  ],
  "taxMode": "SIMPLE_WO"
}
```
---
> Тип операции: возврат расхода
> Тип оплаты: кредит
> Данные покупателя содержат email покупателя
> Тип товара: услуга
> Тип НДС: НДС 20%
> CНО: Единый налог на вмененный доход
```json
{
  "type": "OUTFLOW_REFUND",
  "payments": [
    {
      "type": "CREDIT",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Услуга",
      "quantity": 2,
      "price": 100,
      "type": "SERVICE",
      "tax": "NDS_20"
    }
  ],
  "taxMode": "ENVD"
}
```
---
> Тип операции: приход
> Тип оплаты: встречное предоставление
> Данные покупателя содержат email покупателя
> Тип товара: штучный
> Тип НДС: НДС Расчетная 10%
> CНО: Единый сельскохозяйственный налог
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CONSIDERATION",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_10_CALCULATED"
    }
  ],
  "taxMode": "AGRICULT"
}
```
---
> Тип операции: приход
> Тип оплаты: безналичными
> Данные покупателя содержат email покупателя
> Тип товара: штучный, весовой, обувь, услуга
> Тип НДС: НДС 10%, НДС 20%, НДС расчётная 10%, НДС расчётная 20%
> CНО: Патентная система налогообложения
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 800
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru"
  },
  "total": {
    "priceSum": 800
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_10"
    },
    {
      "name": "Весовой товар",
      "quantity": 2000,
      "price": 100,
      "type": "SCALABLE",
      "tax": "NDS_20"
    },
    {
      "name": "Обувь",
      "quantity": 2,
      "price": 100,
      "type": "SHOES",
      "tax": "NDS_10_CALCULATED"
    },
    {
      "name": "Услуга",
      "quantity": 2,
      "price": 100,
      "type": "SERVICE",
      "tax": "NDS_20_CALCULATED"
    }
  ],
  "taxMode": "PATENT"
}
```
---
> Ниже представлены примеры json массивов с поддерживаемыми реквизитами (тэгами ФФД)
> Каждый пример содержит хотя бы один тэг ФФД
> В чеке может присутствовать несолько тэгов ФФД
> Тэги могут присутствовать как в теле чека, так и в теле конкретной позиции
> Формат данных в значении тэгов регламентируется ФФД и представлен в соответствующих документах

    Тэги ФФД:
    - 1171 [телефон поставщика]
    - 1225 [наименование поставщика]
    - 1226 [ИНН поставщика]
    - 1229 [акциз]
    - 1230 [код страны товара]
    - 1231 [код таможенной декларации]
    - 1057 [признак агента]
    - 1044 [операция платёжного агента]
    - 1005 [адрес оператора перевода]
    - 1016 [ИНН оператора перевода]
    - 1075 [телефон оператора перевода]
    - 1073 [телефон платёжного агента]
    - 1026 [наименование оператора перевода]
    - 1074 [телефон оператора по приёму платежей]
    - 1162 [код товара]
    - 1227 [покупатель]
    - 1228 [ИНН покупателя]
    - 1085 [наименование дополнительного реквизита пользователя]
    - 1086 [значение дополнительного реквизита пользователя]
    - 1191 [дополнительный реквизит предмета расчёта]
    - 1192 [дополнительный реквизит чека (БСО)]
    - 1214 [признак способа расчёта]
    - 1212 [признак предмета расчёта]
    - 1030 [наименование предмета расчёта]
    - 1215 [сумма по чеку (БСО) предоплатой (зачётом аванса и (или) предыдущих платежей)]
    - 777  [сумма предоплаты на позицию] - системный тег - не содержится в ФФД
---
> Банковский агент (позиция)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1057,
          "value": 1
        },
        {
          "tag": 1044,
          "value": "ОП.ПЛ АГЕНТА"
        },
        {
          "tag": 1005,
          "value": "Адрес оператора перевода"
        },
        {
          "tag": 1016,
          "value": "222222222223"
        },
        {
          "tag": 1073,
          "value": "+79101179443"
        },
        {
          "tag": 1075,
          "value": "+79101179444"
        },
        {
          "tag": 1026,
          "value": "Оператор перевода"
        },
        {
          "tag": 1171,
          "value": "+79101179453"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика агента"
        },
        {
          "tag": 1226,
          "value": "999999999990"
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Банковский агент (чек)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX"
    }
  ],
  "tags": [
    {
      "tag": 1057,
      "value": 1
    },
    {
      "tag": 1044,
      "value": "ОП.ПЛ АГЕНТА"
    },
    {
      "tag": 1005,
      "value": "Адрес оператора перевода"
    },
    {
      "tag": 1016,
      "value": "222222222223"
    },
    {
      "tag": 1073,
      "value": "+79101179443"
    },
    {
      "tag": 1075,
      "value": "+79101179444"
    },
    {
      "tag": 1026,
      "value": "Оператор перевода"
    },
    {
      "tag": 1171,
      "value": "+79101179453"
    },
    {
      "tag": 1225,
      "value": "Наименование поставщика агента"
    },
    {
      "tag": 1226,
      "value": "999999999990"
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Банковский платёжный субагент (позиция)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1057,
          "value": 2
        },
        {
          "tag": 1073,
          "value": "+79101179445"
        },
        {
          "tag": 1044,
          "value": "ОП.ПЛ АГЕНТА"
        },
        {
          "tag": 1005,
          "value": "Адрес оператора перевода"
        },
        {
          "tag": 1016,
          "value": "444444444445"
        },
        {
          "tag": 1026,
          "value": "Оператор перевода"
        },
        {
          "tag": 1075,
          "value": "+79101179446"
        },
        {
          "tag": 1171,
          "value": "+79101179453"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика агента"
        },
        {
          "tag": 1226,
          "value": "999999999990"
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Банковский платёжный субагент (чек)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX"
    }
  ],
  "tags": [
    {
      "tag": 1057,
      "value": 2
    },
    {
      "tag": 1073,
      "value": "+79101179445"
    },
    {
      "tag": 1044,
      "value": "ОП.ПЛ АГЕНТА"
    },
    {
      "tag": 1005,
      "value": "Адрес оператора перевода"
    },
    {
      "tag": 1016,
      "value": "444444444445"
    },
    {
      "tag": 1026,
      "value": "Оператор перевода"
    },
    {
      "tag": 1075,
      "value": "+79101179446"
    },
    {
      "tag": 1171,
      "value": "+79101179453"
    },
    {
      "tag": 1225,
      "value": "Наименование поставщика агента"
    },
    {
      "tag": 1226,
      "value": "999999999990"
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Платёжный агент (позиция)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1057,
          "value": 4
        },
        {
          "tag": 1073,
          "value": "+79101179447"
        },
        {
          "tag": 1074,
          "value": "+79101179448"
        },
        {
          "tag": 1171,
          "value": "+79101179453"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика агента"
        },
        {
          "tag": 1226,
          "value": "999999999990"
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Платёжный агент (чек)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX"
    }
  ],
  "tags": [
    {
      "tag": 1057,
      "value": 4
    },
    {
      "tag": 1073,
      "value": "+79101179447"
    },
    {
      "tag": 1074,
      "value": "+79101179448"
    },
    {
      "tag": 1171,
      "value": "+79101179453"
    },
    {
      "tag": 1225,
      "value": "Наименование поставщика агента"
    },
    {
      "tag": 1226,
      "value": "999999999990"
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Платёжный субагент (позиция)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1057,
          "value": 8
        },
        {
          "tag": 1073,
          "value": "+79101179449"
        },
        {
          "tag": 1074,
          "value": "+79101179450"
        },
        {
          "tag": 1171,
          "value": "+79101179453"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика агента"
        },
        {
          "tag": 1226,
          "value": "999999999990"
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Платёжный субагент (чек)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX"
    }
  ],
  "tags": [
    {
      "tag": 1057,
      "value": 8
    },
    {
      "tag": 1073,
      "value": "+79101179449"
    },
    {
      "tag": 1074,
      "value": "+79101179450"
    },
    {
      "tag": 1171,
      "value": "+79101179453"
    },
    {
      "tag": 1225,
      "value": "Наименование поставщика агента"
    },
    {
      "tag": 1226,
      "value": "999999999990"
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Поверенный (позиция)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1057,
          "value": 16
        },
        {
          "tag": 1171,
          "value": "+79101179453"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика агента"
        },
        {
          "tag": 1226,
          "value": "999999999990"
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Поверенный (чек)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX"
    }
  ],
  "tags": [
    {
      "tag": 1057,
      "value": 16
    },
    {
      "tag": 1171,
      "value": "+79101179453"
    },
    {
      "tag": 1225,
      "value": "Наименование поставщика агента"
    },
    {
      "tag": 1226,
      "value": "999999999990"
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Комиссионер (позиция)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1057,
          "value": 32
        },
        {
          "tag": 1171,
          "value": "+79101179453"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика агента"
        },
        {
          "tag": 1226,
          "value": "999999999990"
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Комиссионер (чек)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX"
    }
    ],
  "tags": [
        {
          "tag": 1057,
          "value": 32
        },
        {
          "tag": 1171,
          "value": "+79101179453"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика агента"
        },
        {
          "tag": 1226,
          "value": "999999999990"
        }
      ],
  "taxMode": "DEFAULT"
}
```
---
> Агент (позиция)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1057,
          "value": 64
        },
        {
          "tag": 1171,
          "value": "+79101179453"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика агента"
        },
        {
          "tag": 1226,
          "value": "999999999990"
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Агент (чек)
> Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), 
> наименование поставщика (1225) - опционально.
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX"
    }
  ],
  "tags": [
    {
      "tag": 1057,
      "value": 64
    },
    {
      "tag": 1171,
      "value": "+79101179453"
    },
    {
      "tag": 1225,
      "value": "Наименование поставщика агента"
    },
    {
      "tag": 1226,
      "value": "999999999990"
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Акциз (позиция)
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
    {
      "tag": 1229,
      "value": 3
    },
    {
      "tag": 1230,
      "value": "123"
    },
    {
      "tag": 1231,
      "value": "Код 123"
    }
  ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Код товара (позиция)
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1162,
          "value": "1520043f52d350383277666C345066453973707575"
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Дополнительный реквизит предмета расчёта (позиция)
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1191,
          "value": "Доп. рек. позиции"
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Дополнительный реквизит пользователя (чек)
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX"
    }
  ],
  "tags": [
    {
      "tag": 1085,
      "value": "Доп. рек. пользователя"
    },
    {
      "tag": 1086,
      "value": "Значение доп. рек. пользователя"
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Дополнительный реквизит чека (БСО) (чек)
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX"
    }
  ],
  "tags": [
    {
      "tag": 1192,
      "value": "Доп. реквизит чека (БСО)"
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Признак способа расчёта (предоплата 100 %)(позиция)
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Предоплата 100%",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1214,
          "value": 1
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Признак способа расчёта (предоплата) (позиция)
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Предоплата",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1214,
          "value": 2
        },
        {
          "tag": 777,
          "value": 100
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Признак способа расчёта (аванс)(позиция)
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Аванс",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1214,
          "value": 3
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Признак способа расчёта (полный расчёт)(позиция)
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Полный расчёт",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1214,
          "value": 4
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> сумма по чеку (БСО) предоплатой (зачётом аванса и (или) предыдущих платежей) (чек)
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX"
    }
  ],
  "tags": [
    {
      "tag": 1215,
      "value": 50
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Покупатель и ИНН покупателя (чек)
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX"
    }
  ],
  "tags": [
    {
      "tag": 1227,
      "value": "Покупатель"
    },
    {
      "tag": 1228,
      "value": "123456789012"
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Признак предмета расчёта и наименование предмета расчёта (позиция)
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 200
    }
  ],
  "deviceId": 47098,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79121187552"
  },
  "total": {
    "priceSum": 200
  },
  "positions": [
    {
      "name": "Штучный товар",
      "quantity": 2,
      "price": 100,
      "type": "COUNTABLE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1212,
          "value": 15
        },
        {
          "tag": 1030,
          "value": "3"
        }
      ]
    }
  ],
  "taxMode": "DEFAULT"
}
```
---
> Тестовый пример, включающий все поддерживаемые тэги ФФД в одном чеке
```json
{
  "type": "SALE",
  "payments": [
    {
      "type": "CASHLESS",
      "sum": 1105
    }
  ],
  "deviceId": 96666,
  "timeout": 5,
  "attributes": {
    "email": "fisgo@dreamkas.ru",
    "phone": "+79101179441"
  },
  "total": {
    "priceSum": 1300
  },
  "positions": [
    {
      "type": "COUNTABLE",
      "name": "С банковским агентом",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100,
      "tags": [
        {
          "tag": 1057,
          "value": 1
        },
        {
          "tag": 1171,
          "value": "+79101179442"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика банковского агента"
        },
        {
          "tag": 1226,
          "value": "111111111112"
        },
        {
          "tag": 1044,
          "value": "ОП.ПЛ АГЕНТА"
        },
        {
          "tag": 1005,
          "value": "Адрес оператора перевода"
        },
        {
          "tag": 1016,
          "value": "222222222223"
        },
        {
          "tag": 1073,
          "value": "+79101179443"
        },
        {
          "tag": 1075,
          "value": "+79101179444"
        },
        {
          "tag": 1026,
          "value": "Оператор перевода"
        }
      ]
    },
    {
      "type": "COUNTABLE",
      "name": "С банковским платёжным субагентом",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100,
      "tags": [
        {
          "tag": 1057,
          "value": 2
        },
        {
          "tag": 1171,
          "value": "+79101179445"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика банковского платёжного субагента"
        },
        {
          "tag": 1226,
          "value": "333333333334"
        },
        {
          "tag": 1073,
          "value": "+79101179445"
        },
        {
          "tag": 1044,
          "value": "ОП.ПЛ АГЕНТА"
        },
        {
          "tag": 1005,
          "value": "Адрес оператора перевода"
        },
        {
          "tag": 1016,
          "value": "444444444445"
        },
        {
          "tag": 1026,
          "value": "Оператор перевода"
        },
        {
          "tag": 1075,
          "value": "+79101179446"
        }
      ]
    },
    {
      "type": "COUNTABLE",
      "name": "С платёжным агентом",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100,
      "tags": [
        {
          "tag": 1057,
          "value": 4
        },
        {
          "tag": 1171,
          "value": "+79101179447"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика платёжного агента"
        },
        {
          "tag": 1226,
          "value": "555555555556"
        },
        {
          "tag": 1073,
          "value": "+79101179447"
        },
        {
          "tag": 1074,
          "value": "+79101179448"
        }
      ]
    },
    {
      "type": "COUNTABLE",
      "name": "С платёжным субагентом",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100,
      "tags": [
        {
          "tag": 1057,
          "value": 8
        },
        {
          "tag": 1171,
          "value": "+79101179449"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика платёжного субагента"
        },
        {
          "tag": 1226,
          "value": "666666666667"
        },
        {
          "tag": 1073,
          "value": "+79101179449"
        },
        {
          "tag": 1074,
          "value": "+79101179450"
        }
      ]
    },
    {
      "type": "COUNTABLE",
      "name": "С поверенным",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100,
      "tags": [
        {
          "tag": 1057,
          "value": 16
        },
        {
          "tag": 1171,
          "value": "+79101179451"
        },
        {
          "tag": 1226,
          "value": "777777777778"
        }
      ]
    },
    {
      "type": "COUNTABLE",
      "name": "С комиссионером",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100,
      "tags": [
        {
          "tag": 1057,
          "value": 32
        },
        {
          "tag": 1171,
          "value": "+79101179452"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика комиссионера"
        },
        {
          "tag": 1226,
          "value": "888888888889"
        }
      ]
    },
    {
      "type": "COUNTABLE",
      "name": "С агентом",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100,
      "tags": [
        {
          "tag": 1057,
          "value": 64
        },
        {
          "tag": 1171,
          "value": "+79101179453"
        },
        {
          "tag": 1225,
          "value": "Наименование поставщика агента"
        },
        {
          "tag": 1226,
          "value": "999999999990"
        }
      ]
    },
    {
      "type": "SERVICE",
      "name": "С акцизом",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100,
      "tags": [
        {
          "tag": 1229,
          "value": 3
        },
        {
          "tag": 1230,
          "value": "123"
        },
        {
          "tag": 1231,
          "value": "Код 123"
        }
      ]
    },
    {
      "type": "SHOES",
      "name": "С кодом товара",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100,
      "tags": [
        {
          "tag": 1162,
          "value": "1520043f52d350383277666C345066453973707575"
        }
      ]
    },
    {
      "type": "SERVICE",
      "name": "С дополнительным реквизитом",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100,
      "tags": [
        {
          "tag": 1191,
          "value": "Доп. рек. позиции"
        }
      ]
    },
    {
      "type": "COUNTABLE",
      "name": "Предоплата 100%",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100,
      "tags": [
        {
          "tag": 1214,
          "value": 1
        }
      ]
    },
    {
      "type": "COUNTABLE",
      "name": "Предоплата",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100,
      "tags": [
        {
          "tag": 1214,
          "value": 2
        },
        {
          "tag": 777,
          "value": 5
        }
      ]
    },
    {
      "type": "SERVICE",
      "name": "Без тегов",
      "quantity": 1,
      "tax": "NDS_NO_TAX",
      "price": 100
    },
    {
      "name": "Пени",
      "quantity": 1,
      "price": 12759,
      "type": "SERVICE",
      "tax": "NDS_NO_TAX",
      "tags": [
        {
          "tag": 1212,
          "value": 15
        },
        {
          "tag": 1030,
          "value": "3"
        }
      ]
    }
  ],
  "taxMode": "SIMPLE_WO",
  "tags": [
    {
      "tag": 1085,
      "value": "Доп. рек. пользователя"
    },
    {
      "tag": 1086,
      "value": "Значение доп. рек. пользователя"
    },
    {
      "tag": 1192,
      "value": "Доп. реквизит чека (БСО)"
    },
    {
      "tag": 1227,
      "value": "Клиент"
    },
    {
      "tag": 1228,
      "value": "123456789012"
    },
    {
      "tag": 1215,
      "value": 100
    }
  ]
}
```

**Dreamkas, Saint-Petersburg, Russia 19.12.2019**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
