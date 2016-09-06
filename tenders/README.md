# Дамп бази державних закупівель [z.texty.org.ua](http://z.texty.org.ua)

## Як встановити дамп

1. Встановіть PostgreSQL >=9.5
2. Створіть базу даних `tenders`

```sql
\c postgres
DROP DATABASE IF EXISTS tenders;
CREATE DATABASE tenders;
```
3. Імпортуйте дамп
```sql
psql tenders < z_dump.sql
```

## Опис таблиць

![Схема бази](db.png)

Загалом призначення полів випливають із їх назв. Тому далі будуть описані найнеочевидніші

### `transactions`
Таблиця транзакцій (угод, контрактів)

* `volume` - сума у валюті транзакції
* `volume_uah` - сума у перерахунку на гривню по курсу НБУ на дату транзакції
* `is_vat_included` - чи включено ПДВ
* `prozorro` - id об'єкта [`contract`](http://api-docs.openprocurement.org/en/latest/standard/contract.html) із БД prozorro
* `prozorro_number` - contractID контракту із БД prozorro (наприклад UA-2016-05-20-000180-b-c1)
* `source`
  * `ora` якщо контракт із оракла
  * `prozorro` якщо із prozorro
  * `*.xml` - якщо із xml-дампів вісника 

### `purchases`
Таблиця закупівель. Закупівля, це деяке узагальненя транзакції (угоди). Одна закупівля може мати декілька угод, укладаних із різними постачальниками (sellers), але завжди має єдиного замовника (buyer).

* `goods_name` - предмет закупівлі
* `prozorro` - id об'єкта [`tender`](http://api-docs.openprocurement.org/en/latest/standard/tender.html) із БД prozorro
* `prozorro_number` - tenderID закупівлі із БД prozorro (наприклад UA-2016-05-20-000180-b)
* `source` - джерело даних (аналогічно таблиці transactions)

### `buyers`
Таблиця замовників (покупців)

* `code` - код ЄДРПОУ або ІПН (фізичної або юридичної особи). в окремих випадках вказують іноземні коди

### `sellers`
Таблиця постачальників (продавців)

* `code` - код ЄДРПОУ або ІПН (фізичної або юридичної особи). в окремих випадках вказують іноземні коди

### `bulletins`
Бюлетені вісника державних закупівель (якщо тендер із Зовнішторгвидаву)