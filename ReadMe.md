# VentilationControlHVAC

----
#### Назначение
Графические оболочки (далее по тексту оболочки) управления щитами общеобменных приточно-вытяжных установок **HVAC** (далее по тексту щитами) применяются для дистанционного управления в супервизорном режиме внешних контуров каскадных схем управления аппаратурой **SIEMENS**, **Schneider Electric** с 1999-го года.

Оболочка: 
 - дает команду на автопрогон настроек регулятора внутреннего контура,
 - считывает настройки регуляторов,
 - выдает настройки на регуляторы,
 - выдает задание на регулирование,
 - включает и отключает работу щита.

Регуляторы щитов программные на контроллере щита.
Для управления каждым щитом открывается своя оболочка, на которой вводятся параметры работы.

----
#### Замечания:
 - Сделать на оболочке выбор адреса щита в сети **ModBUS-TCP** (используемых адресов щитов не должно быть в списке доступных),
 - Дописать серверную компоненту (далее по тексту компоненту) опроса щитов по их адресам и раздаче опрошенных данных на формочки по их запросам, индикатор которой вывести например в индикаторы на панели задач,
 - Компонента ведущая (опрашивает), все щиты - ведомые (отвечают на запросы),
 - Вставить на оболочке скрипты-обработчики нажатия кнопок,
 - Внизу подписать на оболочке названия каналов и названия режимов,
 - Сделать из режимов группу, чтобы выбирался только один из них,
 - Делать неактивными виджеты (адрес щита, прочитать/записать настройки щита), которые не могут отдавать команду на щит, когда он в работе,
 - Читать и писать настройки из внешнего **SQL Server**-а по адресу щита в сети **ModBUS-TCP**,
 - Сделать автопрогон настроек регулятора щита, считать их с контроллера в формочку как оптимальных и записать их в базу на внешнем SQL Server-е,
 - Использовать настройки регуляторов щитов, полученные по результатам расчета замкнутой системы регулирования (см. отдельный проект),
 - Переписать расчет переходного процесса замкнутой системы регулирования (см. в отдельный проект) как отдельного клиента с C++ на Python

![IMG_20160928_152215](https://user-images.githubusercontent.com/104857185/169311708-07b7b03a-a0fc-4fd0-a122-0f73b721b21e.jpg)
![IMG_4704](https://user-images.githubusercontent.com/104857185/169308673-81a780ba-8a2d-46db-ab37-a9f41d53fa34.JPG)
![IMG_4486](https://user-images.githubusercontent.com/104857185/169309000-4f485313-a44b-4f15-818e-b0a76adfc1ff.JPG)
![IMG_4547](https://user-images.githubusercontent.com/104857185/169310149-21e65ddf-7baa-45be-a14c-aa3a2d774197.JPG)
![IMG_4778](https://user-images.githubusercontent.com/104857185/169310532-a605a20f-8389-42ef-9c34-928f5b01c33a.JPG)
![IMG_4793](https://user-images.githubusercontent.com/104857185/169310808-5151ae47-95cf-4c17-8756-ea7f3cd65ec5.JPG)
![IMG_3174](https://user-images.githubusercontent.com/104857185/170977221-276454ab-5e53-4747-8108-c8fcff0e6f48.JPG)
![IMG_3176](https://user-images.githubusercontent.com/104857185/170977297-a0bd49e5-281f-4405-9636-5aa8f5c7a8ed.JPG)


#### Примечания:
 - Нужны новые **DDK** и **SDK** фирмы-изготовителя контроллеров HVAC (имеющиеся в наличии работают со старыми моделями аппаратуры), применяемых в щитах.
 - В перспективе переделать с **tk** на **Qt**.
 - В случае использования SCADA-системы фирмы-изготовителя аппаратуры **OPC-сервер** ставится дополнительно поверх нее. Для полноценного функционирования SCADA-систему ставить на **Windows Server** с 4-м **.Net FrameWork**-ом, с **IIS**, с **SQL Express** (после установки зайти в настройки и переподключиться на внешний **SQL Server**). Функционал **OPC-сервер**-а разрешается в USB-вом ключе по дополнительному договору за ежегодную дополнительную оплату фирме-изготовителю.
 - Пользователи работают с программным обеспечением в оригинале с файлового сервера, которое дорабатывается в процессе работы без уведомления его пользователей (в части CI/CD).

Наработки аналогичные SCADA-системе **Desigo Insight** фирмы SIEMENS в том числе:
 * [ИПК Индустрия](https://www.facebook.com/ipkindustriya/) (г. Мытищи) на facebook-е
 * [Симпл-Скада](https://simple-scada.com/) (г. Краснодар) 
 * [Симп Лайт](https://simplight.ru/) (г. Нижний Тагил) 
 * [НПФ Круг](https://www.krug2000.ru/products/ppr/scada-2000.html?utm_medium=cpc&utm_source=mail.yandex.ru&utm_campaign=15353707&utm_term=%D0%BA%D1%83%D0%BF%D0%B8%D1%82%D1%8C%20scada&utm_content=none.0&yclid=2892848951052795745) (г. Пенза)
 * [IECON](https://www.iecon.ru/about/) (г. Москва)
 * [Factory Manager](https://factorymanager.ru/) (г. Омск)
 * [АСУ-Технология](https://factorymanager.ru/) (г. Москва)
 * [MasterSCADA](https://masterscada.ru/?yclid=2966471923235094160#pos) (г. Москва)
 * [FUXA](https://github.com/frangoteam/FUXA) на github-е
 * [Прогресс-Контроль](https://progress-control.ru/) (г. Москва)
 * [Эскон](https://eskon-spb.ru) (г. Санкт-Петенбург)
 * [Инжиниринговые решения](https://ingircompany.ru/siemens?yclid=2798673388731962035) (г. Энгельс)
 * [КОМЕД](https://komed-automation.ru/o-kompanii) (г. Волжский)
 * [ВАРМА](https://varmatech.ru/automation-systems-development/?yclid=2798727833356145209) (г. Санкт-Петенбург)
 * [КАПСТРОЙ](https://constructor.ru/store/constructor/kapstroy/?utm_source=yandex&yclid=2926245293104894532) (г. Москва)
 * [РусКвант](https://rus-kvant.ru/?utm_source=yandex&utm_medium=vitaliy&utm_campaign=yandex_network_brand_rf&utm_content=cid:87412608|gid:5190223231|adid:14101242522|kwid:44651062050&utm_term=%D1%80%D1%83%D1%81%20%D0%BA%D0%B2%D0%B0%D0%BD%D1%82%20%D0%B8%D0%BC%D0%BF%D1%83%D0%BB%D1%8C%D1%81&yclid=2926301674729182146) (г. Москва)
 * [RoomyBots](https://roomybots.ru/doc/)
 * [Advanta](https://promo.advanta-group.ru/promo/?utm_source=yadirect&utm_medium=cpc&utm_campaign=83202387|MK_STRATEGII_KLYUCHI_RF_2023_promo_advanta_group_ru&utm_content=13486473614&utm_term=---autotargeting&yclid=2936916975607943712)
 * [Aston](https://astondevs.ru/?utm_campaign=stranica-retarget&yclid=2937092834591052453)
 * [InSat](https://insat.ru/products/?category=9&yclid=2937160091982435060)
 * [BVL](https://www.programmirovanie-kontrollerov.ru/promo1#block-2) (г. Санкт-Петенбург)
 * [РЕЛЭКС](https://relex.ru/ru/services/?utm_source=yandex&utm_medium=cpc&utm_campaign=cid|RSYA|87558350|context&utm_content=gid|5193206353|aid|14139497941|44738758466|44738758466|desktop|%D0%A1%D0%BE%D1%87%D0%B8&utm_term=%D1%80%D0%B0%D0%B7%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B0%20%D0%B8%D0%BD%D1%84%D0%BE%D1%80%D0%BC%D0%B0%D1%86%D0%B8%D0%BE%D0%BD%D0%BD%D0%BE%D0%B9%20%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B&pm_source=mail.yandex.ru&pm_block=none&pm_position=0&yclid=2980003357856699201) (г. Воронеж)
 * [РидЛаб](https://rydlab.ru/?yclid=3020577673937752289) (г. Свердловск)
 * [Инновационная автоматика](https://iautomatica.ru/catalog-siemens/wincc-7-5/simatic-wincc-odk-v7-5-otkrytyy-komplekt-razrabotchika-odk-optsiya-dlya-simatic-wincc-v7-5-dlya-prog/?utm_source=yandex&utm_medium=cpc&utm_campaign=77346079&yclid=3291318754041991962) (г. Москва)
 * [Институт промышленной автоматизации](https://ipa.sms-a.ru/?utm_source=yandex&utm_medium=cpc&utm_campaign=yarsya&utm_content=4881558151&utm_term=simatic%20step%207%20%D0%BE%D0%B1%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B5&_openstat=ZGlyZWN0LnlhbmRleC5ydTszMDYxMTA2Njs0ODgxNTU4MTUxO21haWwueWFuZGV4LnJ1Omd1YXJhbnRlZQ&yclid=3573652583933350514) (г. Самара)
 * [ГК ПромИнвест](https://prominvest-36.ru/import/siemens?yclid=3750995521149670230) (г. Воронеж)

#### Ссылочная литература
Каталоги 1998-го (остался только в печатном виде), 2002-го и 2005-го годов на сервере в папках:
 - `P:\Техническая информация\Электротехника и КИПиА\SIEMENS`
 - `P:\Техническая информация\Электротехника и КИПиА\SIEMENS\Synco HVAC`
 - `P:\Техническая информация\Электротехника и КИПиА\Schneider Electric` 

Техническая документация по SCADA-системам фирмы-изготорителя на сервере в папках:
 - `P:\Техническая информация\Электротехника и КИПиА\SIEMENS\Desigo Insight`
 - `P:\Техническая информация\Электротехника и КИПиА\SIEMENS\Desigo CC`
 - `P:\Техническая информация\Электротехника и КИПиА\SIEMENS\Cerberus Pro`
 - `P:\Техническая информация\Электротехника и КИПиА\SIEMENS\DMS8000`
 - `P:\Техническая информация\Электротехника и КИПиА\SIEMENS\SCADA Win CC`
 - `P:\Техническая информация\Электротехника и КИПиА\SIEMENS\SiPass`
