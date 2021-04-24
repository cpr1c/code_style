# Соглашение о кодировании

Текст содержит минимальный набор требований к оформлению кода. Более полные требования описаны тут https://its.1c.ru/db/v8std

[Настройки EDT для работы](edt_settings.md)

[Правила комментирования кода](Комментирование%20кода.md)

# Именование метаданных

## Имя объекта
Рекомендуется строить на основе синонима: пробелы и пр. недопустимые в имени символы, удаляются, а первые буквы слов делаются прописными.

Например, ***неправильно***:
- у справочника **НаборыДополнительныхРеквизитовИСведений** задан синоним «Дополнительные свойства»
- у общей команды **ПрисоединенныеФайлы** – синоним «Файлы присоединенные»;

***правильно***:
- у справочника **НаборыДополнительныхРеквизитовИСведений** задан синоним «Наборы дополнительных реквизитов и сведений»
- у общей команды **ПрисоединенныеФайлы** – синоним «Присоединенные файлы».

Также допустимы ситуации, когда имя более кратко описывает объект, чем синоним – когда в имени «сокращены» одно или несколько последних «малозначащих» слов из синонима. Например:

- **ДлительностьОжиданияСервера** – синоним «Длительность ожидания сервера (сек)»
- **КоличествоЕдиниц** – синоним «Количество единиц измерения»
- **Обработки.ГрупповоеИзменениеОбъектов.Операции.ИмяРеквизита** – синоним «Имя реквизита (свойство)»

Имя также может не включать союзы и предлоги из текста синонима, например: для реквизита **ЗначениеСкидкиНаценки** синоним «*Значение скидки или наценки*».

А также наоборот, допустимы ситуации, когда синоним более кратко описывает объект, чем имя – когда в синониме «сокращены» одно или несколько последних «технических» слов из имени.

Данное требование продиктовано тем соображением, что объекты конфигурации и их представления в пользовательском интерфейсе должны быть максимально легко узнаваемыми.

#### ВАЖНО! Новые объекты, добавленные в типовую конфигурацию должны содержать префикс ЦПР_

## Синоним объекта
Должен быть определен так, чтобы осмысленно, лаконично описывать объект. Заполняется обязательно.

Не рекомендуется в синонимах объектов использовать сокращения. Исключением являются только общеупотребительные и соответствующие целевой аудитории сокращения (например, Сумма (регл.) ) и аббревиатуры (например, НДС или МСФО).

В синонимах объектов и текстовых сообщениях пользователю должны использоваться общепринятые термины, понятные пользователю. Не должно быть сленга, искажения названий продуктов и компаний; англоязычных фраз, записанных русскими буквами; русскоязычных английскими буквами и т.п.

# Оформление модулей

* Длина строки в общем случае не должна превышать **120** символов.
* Текст модуля должен быть оформлен синтаксическим отступом. Для синтаксического отступа используется табуляция
* Одна строка кода - одна управляющая конструкция.
 
```bsl
// Плохо:
Если ЭтоБрак Тогда Продолжить; КонецЕсли;

// Хорошо:
Если ЭтоБрак Тогда
  Продолжить;
КонецЕсли;
```
* Следует отделять друг от друга пробелами ключевые слова, вызовы процедур и функций, параметры процедур и функций внутри скобок, операторы.

```bsl
// Плохо:
Сообщить(“Сумма: “+Сумма);

// Хорошо:
Сообщить(“Сумма: “ + Сумма);
```

* Для разделения на логические части внутри модуля следует использовать пустые строки
* При вызове функции с несколькими параметрами при переносе строк необходимо выравнивать параметры по первому

```bsl
// Начальное состояние (строка слишком длинная):
НалоговыйУчет.ОстаткиВременныхРазниц(СтрокаВидАктиваОбязательства, СписокОрганизаций, Реквизиты.НачалоГода, Реквизиты.КонДата);

// Плохо:
НалоговыйУчет.ОстаткиВременныхРазниц(
    СтрокаВидАктиваОбязательства, СписокОрганизаций, Реквизиты.НачалоГода, Реквизиты.КонДата);

// Лучше:
НалоговыйУчет.ОстаткиВременныхРазниц(СтрокаВидАктиваОбязательства,
                                     СписокОрганизаций,
                                     Реквизиты.НачалоГода,
                                     Реквизиты.КонДата);

// Хорошо:
НалоговыйУчет.ОстаткиВременныхРазниц(
    СтрокаВидАктиваОбязательства,
    СписокОрганизаций,
    Реквизиты.НачалоГода,
    Реквизиты.КонДата);
    
```

* Выравнивание однотипных операторов. При следовании друг за другом нескольких однотипных операторов допускается их выравнивание. 

```bsl
// Хорошо:
НоваяСтрока = ВидыОпераций.Добавить();
НоваяСтрока.ВидОперации         = ВидОперации;
НоваяСтрока.НомерГруппы         = ГруппаПоВидуОперации(ВидОперации);
НоваяСтрока.ПоОрганизацииВЦелом = ГруппаПоОрганизации(НоваяСтрок);
```

* Модуль должен быть оформлен в соответствии с рекомендациями от 1С https://its.1c.ru/db/v8std#content:455:hdoc

# Структура модулей
* В программном модуле (общие модули, модули объектов, модули менеджеров объектов, модули форм, команд и т.п.) в общем случае могут присутствовать следующие разделы в приведенной ниже последовательности:

1. заголовок модуля -представляет собой комментарий в самом начале модуля. В заголовке модуля приводится его краткое описание и условия применения
```bsl
////////////////////////////////////////////////////////////////////////////////
// Клиентские процедуры и функции общего назначения:
// - для работы со списками в формах;
// - для работы с журналом регистрации;
// - для обработки действий пользователя в процессе редактирования
//   многострочного текста, например комментария в документах;
// - прочее.
//  
////////////////////////////////////////////////////////////////////////////////
```
2. раздел описания переменных
1. экспортные процедуры и функции модуля, составляющие его программный интерфейс
1. обработчики событий объекта (формы)
1. служебные процедуры и функции модуля
1. раздел инициализации

* Объемные разделы модулей рекомендуется разбивать на подразделы по функциональному признаку.

* Разделы и подразделы оформляются в виде областей. При этом имена областей должны удовлетворять требованиям стандарта Правила образования имен переменных
* В модуле не должно быть пустых областей

## Общий модуль

```bsl
#Область ПрограммныйИнтерфейс
// содержит экспортные процедуры и функции, предназначенные для использования другими объектами конфигурации или другими программами (например, через внешнее соединение).
#КонецОбласти

#Область СлужебныйПрограммныйИнтерфейс
// предназначен для модулей, которые являются частью некоторой функциональной подсистемы. В нем должны быть размещены экспортные процедуры и функции, которые допустимо вызывать только из других функциональных подсистем этой же библиотеки.
#КонецОбласти

#Область СлужебныеПроцедурыИФункции
// содержит процедуры и функции, составляющие внутреннюю реализацию общего модуля. В тех случаях, когда общий модуль является частью некоторой функциональной подсистемы, включающей в себя несколько объектов метаданных, в этом разделе также могут быть размещены служебные экспортные процедуры и функции, предназначенные только для вызова из других объектов данной подсистемы.
#КонецОбласти
```

## Модули объектов, менеджеров, наборов записей, обработок, отчетов и т.п.

```bsl
#Область ОписаниеПеременных

#КонецОбласти

#Область ПрограммныйИнтерфейс
// Код процедур и функций
#КонецОбласти

#Область ОбработчикиСобытий
// содержит обработчики событий модуля объекта (ПриЗаписи, ПриПроведении и др.)
#КонецОбласти

#Область СлужебныйПрограммныйИнтерфейс
// Код процедур и функций
#КонецОбласти

#Область СлужебныеПроцедурыИФункции
//  Код процедур и функций
#КонецОбласти

#Область Инициализация

#КонецОбласти
```

## Модули форм
```bsl
#Область ОписаниеПеременных

#КонецОбласти

#Область ОбработчикиСобытийФормы
// Код процедур и функций
#КонецОбласти

#Область ОбработчикиСобытийЭлементовШапкиФормы
// Код процедур и функций
#КонецОбласти

#Область ОбработчикиСобытийЭлементовТаблицыФормы<ИмяТаблицыФормы>
// Код процедур и функций
#КонецОбласти

#Область ОбработчикиКомандФормы
// Код процедур и функций
#КонецОбласти

#Область СлужебныеПроцедурыИФункции
// Код процедур и функций
#КонецОбласти
```

## Модули команд
```bsl
#Область ОбработчикиСобытий
// Код процедур и функций
#КонецОбласти

#Область СлужебныеПроцедурыИФункции
// Код процедур и функций
#КонецОбласти
```

# Имена процедур и функций
Правильный выбор имен процедур и функций очень важен для повышения читаемости кода. В большинстве случаев хорошо выбранное имя процедуры в сочетании с правильно подобранными именами параметров избавляют от необходимости ее как-то дополнительно описывать. В ряде случаев, сложности в выборе имени процедуры и (или) ее параметров свидетельствуют о неправильной архитектуре программного кода. И наоборот, если "самодокументирующееся" имя придумать легко, значит процедура спроектирована правильно.

* Имена процедур, функций и формальных параметров следует образовывать от терминов предметной области таким образом, чтобы из имени было понятно назначение. Следует стремиться к тому, чтобы имена были "говорящими" (документировали сами себя).

Плохо:
```bsl
Функция ВыполнитьПроверку(Параметр1, Рекв, ТЗ)
Функция ПолучитьМассивыРеквизитов(ХозяйственнаяОперация, МассивВсехРеквизитов, МассивРеквизитовОперации)
```

Хорошо:
```bsl
Функция РеквизитОбъектаЗаданногоТипа(Объект, ИмяРеквизита, ТипЗначения)
Функция ИменаРеквизитовПоХозяйственнойОперации(ХозяйственнаяОперация, ИменаВсеРеквизиты, ИменаРеквизитыОперации)
```

* Имена следует образовывать путем удаления пробелов между словами. При этом, каждое слово в имени пишется с прописной буквы. Предлоги и местоимения из одной буквы также пишутся прописными буквами.
* Не рекомендуется в названиях процедур и функций описывать типы принимаемых параметров и (или) возвращаемых значений
Плохо:
```bsl
Функция ПолучитьМассивРолейСПравомДобавления()
Функция ПолучитьСтруктуруДополнительныхНастроек()
```

Хорошо:
```bsl
Функция ИменаРолейСПравомДобавления()
Функция ДополнительныеНастройки()
```

* Имена процедур в общем случае, следует образовывать от неопределенной формы глагола, от сути выполняемого действия

Плохо:
```bsl
Процедура ЗагрузкаКонтрагента()
```

Хорошо:
```bsl
Процедура ЗагрузитьКонтрагента()
```
* Имена функций в общем случае следует образовывать от описания возвращаемого значения.

Плохо:
```bsl
Функция ПолучитьПолноеИмяПользователя() 
Функция СоздатьПараметрыЗаполненияЦенПоставщика() 
Функция ОпределитьДатуНачалаСеанса()
```

Хорошо:
```bsl
Функция ПолноеИмяПользователя() 
Функция НовыеПараметрыЗаполненияЦенПоставщика() 
Функция ДатаНачалаСеанса()
```

* Параметр функции не должен возвращать значение. Иными словами не используйте входные параметры функций как дополнительный вывод. Весь вывод должен быть в возвращаемом значении. Если нужно возвращать несколько значений следует использовать такие типы как `Структура`, `Массив` и т.д.
```bsl
// Плохо:
URLСервиса = "";
ИмяПользователя = "";
ПарольПользователя = "";

ЗаполнитьПараметрыПодключения(URLСервиса, ИмяПользователя, Пароль);

// Хорошо:
ПараметрыПодключения = ПолучитьПараметрыПодключения();
// Возвращаемое значение - структура:
//     URLСервиса         - Строка
//     ИмяПользователя    - Строка
//     ПарольПользователя - Строка
```

* Не используйте отрицание в именах переменных и методов
```bsl
// Плохо:
Функция ПроверкаНеПройдена()
...

Если Не (Условие И Не ПроверкаНеПройдена()) Тогда

// Хорошо:
Функция ПроверкаПройдена()
...

Если Не Условие И Не ПроверкаПройдена() Тогда
```

# Условия
* Предпочтительней использовать тернарный оператор для простых конструкций.
```bsl
// Плохо:
Если НДС0 Тогда
    Возврат 0;
Иначе
    Возврат 18;
КонецЕсли;

// Хорошо:
Возврат ?(НДС0, 0, 18);
```

* Не допускайте использования вложенных тернарных операторов.
* Ключевое слово `Тогда` пишется на той же строке, что и последнее условие.
* Сложные условия (содержащие 3  конструкции и более) необходимо выносить в отдельные методы.

```bsl
// Плохо:
Если ИдентификаторОбъекта = "АнализСубконто"
    ИЛИ ИдентификаторОбъекта = "АнализСчета"
    ИЛИ ИдентификаторОбъекта = "ОборотноСальдоваяВедомость"
    ИЛИ ИдентификаторОбъекта = "ОборотноСальдоваяВедомостьПоСчету"
    ИЛИ ИдентификаторОбъекта = "ОборотыМеждуСубконто"
    ИЛИ ИдентификаторОбъекта = "ОборотыСчета"
    ИЛИ ИдентификаторОбъекта = "СводныеПроводки" 
    ИЛИ ИдентификаторОбъекта = "ГлавнаяКнига"
    ИЛИ ИдентификаторОбъекта = "ШахматнаяВедомость" Тогда
    ПараметрыРасшифровки.Вставить("ОткрытьОбъект", Ложь);
		
    ЕстьПоказатель  = Ложь;
    ЕстьКорЗначение = Ложь;
    ЕстьСчет        = Истина;
    Счет            = Неопределено;
    ПервыйЭлемент   = Неопределено;
КонецЕсли;

// Хорошо:
Если ОткрыватьОбъектПриИдентификаторе(ИдентификаторОбъекта) Тогда
    ПараметрыРасшифровки.Вставить("ОткрытьОбъект", Ложь);
		
    ЕстьПоказатель  = Ложь;
    ЕстьКорЗначение = Ложь;
    ЕстьСчет        = Истина;
    Счет            = Неопределено;
    ПервыйЭлемент   = Неопределено;
КонецЕсли;

Функция ОткрыватьОбъектПриИдентификаторе(ИдентификаторОбъекта)
	
    Возврат ИдентификаторОбъекта = "АнализСубконто"
        ИЛИ ИдентификаторОбъекта = "АнализСчета"
        ИЛИ ИдентификаторОбъекта = "ОборотноСальдоваяВедомость"
        ИЛИ ИдентификаторОбъекта = "ОборотноСальдоваяВедомостьПоСчету"
        ИЛИ ИдентификаторОбъекта = "ОборотыМеждуСубконто"
        ИЛИ ИдентификаторОбъекта = "ОборотыСчета"
        ИЛИ ИдентификаторОбъекта = "СводныеПроводки" 
        ИЛИ ИдентификаторОбъекта = "ГлавнаяКнига"
        ИЛИ ИдентификаторОбъекта = "ШахматнаяВедомость";

КонецФункции
```

* Избегайте использование Йода-синтаксиса.
```bsl
// Плохо:
Если 0 = Сумма Тогда

// Хорошо:
Если Сумма = 0 Тогда
```

# Переменные

* Имена переменных следует образовывать от терминов предметной области таким образом, чтобы из имени переменной было понятно ее назначение.

* Имена следует образовывать путем удаления пробелов между словами. При этом, каждое слово в имени пишется с прописной буквы. Предлоги и местоимения из одной буквы также пишутся прописными буквами

Плохо:
```bsl
масРеквизитов, соотвВидИмя, новСтр, Струк
```

Хорошо:
```bsl
  Перем ДиалогРаботыСКаталогом;     // Диалог работы с каталогом   
  Перем КоличествоПачекВКоробке;    // Количество пачек в коробке
```

* Имена переменных запрещается начинать с подчеркивания
* Имена переменных не должны состоять из одного символа. Использование односимвольных имен переменных допускается только для счетчиков циклов.
* Переменные, отражающие состояние некоторого флага, следует называть так, как пишется истинное значение этого флага

Плохо:
```bsl
  Перем ГалкаОшибка;        
  Перем ФлагТара;   
```
Хорошо:
```bsl
  Перем ЕстьОшибки;     // Признак наличия ошибок в процедуре.   
  Перем ЭтоТоварТара;   // Признак, что товар относится к возвратной таре.
```

* Избегайте неявного определения переменных
```bsl
// Плохо
Функция ИдентификаторОбъекта(Объект)
    // Ошибки не будет, даже если переменная не определена в области видимости.
    // В результате будет определена переменная со значением Неопределено.
    ВашаПеременная = ВашаПеременная;
    
    Если Не ЗначениеЗаполнено(ВашаПеременная) Тогда
        ...
    КонецЕсли;
КонецФункции

// Хорошо
Функция ИдентификаторОбъекта(Объект)
    Перем ВашаПеременная;
    ...
КонецФункции
```
* Не используйте отрицание в именах переменных и методов
```bsl
// Плохо:
Функция ПроверкаНеПройдена()
...

Если Не (Условие И Не ПроверкаНеПройдена()) Тогда

// Хорошо:
Функция ПроверкаПройдена()
...

Если Не Условие И Не ПроверкаПройдена() Тогда
```

# Комментарии
* Если код требует комментария для пояснения работы - в первую очередь необходимо рассмотреть варианты рефакторинга, чтобы код не требовал комментария.
* К комментариям также относятся ограничения на длину строки в 120 символов.
* В модулях не должно быть закомментированного кода

# Спасибо
https://github.com/skyksandr/1c-styleguide
