# FisGo API

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

# Описание API внешних чеков платформы FisGo
Внешний чек "external_purchase" - чек для фискализации, поступающий через Poll API
[https://viki3.docs.apiary.io/#reference/poll-api/external-purchase/example]

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
##### Банковский агент (позиция / чек)
Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), наименование поставщика (1225) - опционально.
```json
{
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
```
##### Банковский платёжный субагент (позиция / чек)
Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), наименование поставщика (1225) - опционально.
```json
{
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
```
##### Платёжный агент (позиция / чек)
Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), наименование поставщика (1225) - опционально.
```json
{
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
```

##### Платёжный субагент (позиция / чек)
Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), наименование поставщика (1225) - опционально.
```json
{
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
```
##### Поверенный (позиция / чек)
Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), наименование поставщика (1225) - опционально.
```json
{
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
```
##### Комиссионер (позиция / чек)
Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), наименование поставщика (1225) - опционально.
```json
{
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
```
##### Агент (позиция / чек)
Примечание: необходимо также передать ИНН поставщика (1226) и тел. номер поставщика (1171), наименование поставщика (1225) - опционально.
```json
{
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
```
##### Данные поставщика (позиция / чек)

```json
{
  "tags": [
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
```
##### Акциз (позиция)

```json
{
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
```
##### Код товара (позиция)

```json
{
  "tags": [
    {
      "tag": 1162,
      "value": "1520043f52d350383277666C345066453973707575"
    }
  ]
}
```
##### Дополнительный реквизит предмета расчёта (позиция)

```json
{
  "tags": [
    {
      "tag": 1191,
      "value": "Доп. рек. позиции"
    }
  ]
}
```
##### Дополнительный реквизит пользователя (чек)

```json
{
  "tags": [
    {
      "tag": 1085,
      "value": "Доп. рек. пользователя"
    },
    {
      "tag": 1086,
      "value": "Значение доп. рек. пользователя"
    }
  ]
}
```
##### Дополнительный реквизит чека (БСО) (чек)

```json
{
  "tags": [
    {
      "tag": 1192,
      "value": "Доп. реквизит чека (БСО)"
    }
  ]
}
```
##### Признак способа расчёта (позиция)

```json
{
  "tags": [
    {
      "tag": 1214,
      "value": 1
    }
  ]
}
```
##### Признак способа расчёта (предоплата) (позиция)

```json
{
  "tags": [
    {
      "tag": 1214,
      "value": 2
    },
    {
      "tag": 777,
      "value": 5000
    }
  ]
}
```
##### сумма по чеку (БСО) предоплатой (зачётом аванса и (или) предыдущих платежей) (чек)

```json
{
  "tags": [
    {
      "tag": 1215,
      "value": 10000
    }
  ]
}
```
##### Покупатель и ИНН покупателя (чек)

```json
{
  "tags": [
    {
      "tag": 1227,
      "value": "Покупатель"
    },
    {
      "tag": 1228,
      "value": "123456789012"
    }
  ]
}
```
##### Признак предмета расчёта и наименование предмета расчёта (позиция)

```json
{
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
```
##### Тестовый пример, включающий все поддерживаемые тэги ФФД в одном чеке

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
    "email": "m.savchenko@dreamkas.ru",
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
      "value": "Савченко Михаил Андреевич"
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
