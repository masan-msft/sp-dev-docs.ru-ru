# <a name="ipropertypanefield-tproperties-interface"></a>Интерфейс <TProperties> IPropertyPaneField



_Параметры типов: `<TProperties>`_



Поле PropertyPane.




## <a name="properties"></a>Свойства

| Свойство     | Тип   | Описание|
|:-------------|:-------|:-----------|
|`properties`      | `TProperties` | Объект строго типизированных свойств. Зависит от типа поля. Пример. У компонента Checkbox — реквизиты ICheckboxProps, у компонента TextField — реквизиты ITextField. |
|`shouldFocus`      | `boolean` | Указывает, должен ли на этом элементе управления находится фокус. Значение по умолчанию — false. |
|`targetProperty`      | `string` | Целевое свойство из контейнера свойств веб-части. |
|`type`      | [`PropertyPaneFieldType`](../sp-webpart-base/propertypanefieldtype.md) | Тип поля PropertyPane. |






