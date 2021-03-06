# Протоколи розкриття з Вісника держзакупівель 

Цей датасет утворений з дампу бази даних Вісника держзакупівель зробленого на початку 2015 року. Ми витягнули дані про учасників  торгів та їх ставки із файлів протоколів розкриття цін. Інформація про всі тендери до початку 2015 року. На основі цього датасету був написаний матеріал-дослідження про схеми на тендерах http://z.texty.org.ua/protocols/ 

## Скачати CSV
http://z.texty.org.ua/data/protocols.unnested.csv.gz


## Що у цих даних?
Це дані отримані із файлів протоколів розкриття цін, що містяться у базі Вісника державних закупівель. 

## Опис основних стовпців
Значна частина полів містять посилання на закупівлю, контракт, замовника, переможця у дампі бази закупівель, який можна скачати [за лінком](../)


### Поля спільні для усього тендера (дублюються для цінових пропозицій з одного тендера)

* `purchase_id` - id закупівлі в базі вісника. Можна використовувати щоб отримати інформацію про неї за лінком https://ips.vdz.ua/ua/purchase_details.htm?id=<purchase_id>
* `doc_id` - id документу в базі вісника.
* `announce_id` - id оголошення в базі візника
* `seller_id` - id переможця (продавця) у базі z.texty.org.ua. Можна використовувати щоб отримати інформацію про неї за лінком http://z.texty.org.ua/seller/<seller_id>
* `contract_id` - id угоди у базі z.texty.org.ua. Можна використовувати щоб отримати інформацію про неї за лінком http://z.texty.org.ua/deal/<contract_id>
* `volume` - сума у валюті транзакції
* `volume_uah` - сума у перерахунку на гривню по курсу НБУ на дату транзакції
* `winner.name` - назва переможця
* `winner.code` - код переможця (ЄДРПОУ, ІПН)
* `buyer_id` - id замовника (покупця) у базі z.texty.org.ua. Можна використовувати щоб отримати інформацію за лінком http://z.texty.org.ua/buyer/<buyer_id>
* `buyer_name` - назва замовника
* `buyer_code` - код замовника (ЄДРПОУ, ІПН)
* `region_id` - id регіону замовника
* `purchase_cost` - вартість оголошена замовником у валюті 
* `purchase_cost_uah` - вартість оголошена замовником у гривні
* `contract_date` - дата угоди
* `winner_region_id` - регіон переможця
* `part.num` - кількість пропозицій
* `lowest.price.won` - TRUE якщо перемогла найнижча ціна

### Поля із протоколів розкриття цінових пропозицій 

* `date` - оригінальний текст із стовпця '№ п.п., дата'
* `firm` - оригінальний текст із стовця 'назва учасника' 
* `docs` - оригінальний текст із стовця 'наявність документів'
* `price` - оригінальний текст із стовця 'ціна пропозиції'
* `notes` - оригінальний текст із стовця 'примітки'
* `edrpou` - розпізнаний код ЄДРПОУ
* `ipn` - розпізнаний код ІПН
* `valid.edrpou` - TRUE якщо ЄДРПОУ проходить алгоритмічну перевірку на правильність
* `valid.ipn` - TRUE якщо ІПН проходить алгоритмічну перевірку на правильність
* `price.extr` - розпізнана ціна пропозиції
* `code` - код (якщо є - ЄДРПОУ, інакше ІПН)
* `seller_region_id` - регіон учасника (на основі поштових індексів вказаних у адресі з ЄДР)
* `winner` - TRUE якщо учасник переміг у тендері

