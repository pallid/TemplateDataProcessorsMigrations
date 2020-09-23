# Шаблон обработки для выполнения миграция и настроек по локальным и облачным базам (TemplateDataProcessorsMigrations)

Обработка представлена как шаблон для выполнения миграция и настроек по локальным и облачным базам

### Инструкция по применению обработки:
- открыть обработку под неразделенным пользователем


        Выполнение по определенным областям:
        - установить Вариант обработки разделенных данных как Выборочные области
        - указать необходимую область через разделитель запятая

        По всем областям:
        - установить Вариант обработки разделенных данных как Все области

-  нажать команду **Выполнить настройки** 
- проанализировать протокол по завершению настройки

![](./assets/log.png)

### Пример реализации настройки

необходимо описать логику настройки в методе `ВыполнитьНастройкиСлужебная` в модуле объекта 

```bsl
Процедура ВыполнитьНастройкиСлужебная(Результат, пОбласть=Неопределено) Экспорт
	
	Попытка
		// Вставить код с полезной нагрузкой
		Текст = "Информационное сообщение положительного результата работы";
		Результат.ПротоколРаботы.Добавить(Текст);
	Исключение
		ТекстОшибки = ПодробноеПредставлениеОшибки(ИнформацияОбОшибке());
		Результат.ПротоколРаботы.Добавить(ТекстОшибки);
		Результат.ЕстьОшибки = Истина;
	КонецПопытки;
	
КонецПроцедуры
```

**Пример** 

в примере будет показано как изменить значение константы `ЗаголовокСистемы` во всех областях

```bsl
Процедура ВыполнитьНастройкиСлужебная(Результат, пОбласть=Неопределено) Экспорт
	
	Попытка
		Заголовок = Константы.ЗаголовокСистемы.Получить();
        	НовыйЗаголовок = "[ТЕСТОВАЯ] " + Заголовок;
        	Константы.ЗаголовокСистемы.Записать(НовыйЗаголовок);
	Исключение
		ТекстОшибки = ПодробноеПредставлениеОшибки(ИнформацияОбОшибке());
		Результат.ПротоколРаботы.Добавить(ТекстОшибки);
		Результат.ЕстьОшибки = Истина;
	КонецПопытки;
	
КонецПроцедурым
```

**[СКАЧАТЬ](https://github.com/pallid/TemplateDataProcessorsMigrations/releases/latest)**
