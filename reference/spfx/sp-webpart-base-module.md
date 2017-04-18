# <a name="sp-webpart-base-module"></a>Модуль sp-webpart-base



## <a name="classes"></a>Классы

| Класс    |  Описание |
|:-------------|:---------------|
| [`BaseClientSideWebPart`](./sp-webpart-base/baseclientsidewebpart.md)     | В этом абстрактном классе реализованы основные функции клиентской веб-части. Каждая клиентская веб-часть должна наследоваться от этого класса. Помимо основных функций, этот класс предоставляет некоторые API, которые может использовать веб-часть. Эти API делятся на две категории. API первой категории предоставляют данные и функции. Пример: контекст веб-части (т .е. this.context). Этот API следует использовать для доступа к контекстным данным, относящимся к данному экземпляру веб-части. API второй категории предоставляют базовую версию для жизненного цикла веб-части и могут быть переопределены для обновленной версии. render() — это единственный API, который должен быть реализован или переопределен веб-частью. У всех остальных API жизненного цикла есть базовая версия. Их можно переопределять в соответствии с потребностями веб-части. Чтобы принять правильное решение, обратитесь к документации по отдельным API. |



## <a name="interfaces"></a>Интерфейсы

| Интерфейс    |  Описание |
|:-------------|:---------------|
| [`IClientSideWebPartStatusRenderer`](./sp-webpart-base/iclientsidewebpartstatusrenderer.md)   | Интерфейс, реализуемый компонентом, который должен отображать индикатор загрузки и сообщения об ошибках для веб-части.  |
| [`IPlaceholderProps`](./sp-webpart-base/iplaceholderprops.md)   | Используется для отображения заполнителя в случае отсутствия содержимого или наличия временного содержимого. Кнопка необязательна.  |
| [`IPlaceholderSpinnerProps`](./sp-webpart-base/iplaceholderspinnerprops.md)   | Интерфейс для свойств, используемых для отображения индикатора загрузки в области просмотра веб-части.  |
| [`IPropertyPaneButtonProps`](./sp-webpart-base/ipropertypanebuttonprops.md)   | Свойства кнопки PropertyPane.  |
| [`IPropertyPaneCheckboxProps`](./sp-webpart-base/ipropertypanecheckboxprops.md)   | Свойства компонента CheckBox в PropertyPane.  |
| [`IPropertyPaneChoiceGroupOption`](./sp-webpart-base/ipropertypanechoicegroupoption.md)   | Свойства параметра ChoiceGroup в PropertyPane.  |
| [`IPropertyPaneChoiceGroupProps`](./sp-webpart-base/ipropertypanechoicegroupprops.md)   | Свойства объекта ChoiceGroup в PropertyPane.  |
| [`IPropertyPaneConfiguration`](./sp-webpart-base/ipropertypaneconfiguration.md)   | Параметры конфигурации веб-части  |
| [`IPropertyPaneCustomFieldProps`](./sp-webpart-base/ipropertypanecustomfieldprops.md)   | Свойства объекта CustomPropertyField в PropertyPane.  |
| [`IPropertyPaneDropdownOption`](./sp-webpart-base/ipropertypanedropdownoption.md)   | Пункты раскрывающегося меню PropertyPane.  |
| [`IPropertyPaneDropdownProps`](./sp-webpart-base/ipropertypanedropdownprops.md)   | Свойства компонента раскрывающегося меню PropertyPane.  |
| [`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)   | Поле PropertyPane.  |
| [`IPropertyPaneGroup`](./sp-webpart-base/ipropertypanegroup.md)   | Группа PropertyPane. Группа является частью PropertyPanePage.  |
| [`IPropertyPaneLabelProps`](./sp-webpart-base/ipropertypanelabelprops.md)   | Свойства компонента PropertyPaneLabel.  |
| [`IPropertyPaneLinkProps`](./sp-webpart-base/ipropertypanelinkprops.md)   | Свойства компонента PropertyPaneLink.  |
| [`IPropertyPanePage`](./sp-webpart-base/ipropertypanepage.md)   | Интерфейс PropertyPanePage.  |
| [`IPropertyPanePageHeader`](./sp-webpart-base/ipropertypanepageheader.md)   | Заголовок PropertyPane. Этот заголовок остается неизменным для всех страниц.  |
| [`IPropertyPaneSliderProps`](./sp-webpart-base/ipropertypanesliderprops.md)   | Свойства компонента PropertyPaneSliderProps.  |
| [`IPropertyPaneTextFieldProps`](./sp-webpart-base/ipropertypanetextfieldprops.md)   | Свойства компонента PropertyPaneTextField.  |
| [`IPropertyPaneToggleProps`](./sp-webpart-base/ipropertypanetoggleprops.md)   | Свойства компонента PropertyPaneToggle.  |
| [`ISerializedServerProcessedData`](./sp-webpart-base/iserializedserverprocesseddata.md)   | Содержит наборы данных, которые могут обрабатываться серверными службами, например службами индексирования поиска и корректировки ссылок.  |
| [`ISerializedWebPartData`](./sp-webpart-base/iserializedwebpartdata.md)   | Эта структура представляет часть сериализованного состояния веб-части, которым управляет веб-часть. Ее дополняет интерфейс IWebPartData, который содержит данные, добавляемые платформой к сериализованным данным.  |
| [`IWebPartContext`](./sp-webpart-base/iwebpartcontext.md)   | Интерфейс базового контекста для клиентских веб-частей.  |
| [`IWebPartData`](./sp-webpart-base/iwebpartdata.md)   | Эта структура представляет собой сериализованное состояние веб-части. Эта структура возвращается в результате вызова API serialize() в веб-части. Структура поля properties относится к веб-части. Каждая веб-часть может выбрать набор свойств для сериализации.  |
| [`IWebPartPropertiesMetadata`](./sp-webpart-base/iwebpartpropertiesmetadata.md)   | Используйте эту структуру, чтобы определить метаданные для свойств веб-части как сопоставление строки с IWebPartPropertyMetadata. Ключ — это путь json к свойству веб-части. Путь json поддерживает следующие операторы: – точка (.) для выбора элементов объекта, например person.name – квадратные скобки ([]) для выбора элементов массива, например person.photoURLs[0] – звездочка в квадратных скобках [*] в качестве подстановочного знака элементов массива, например person.websites[*]. Эти операторы можно сочетать, например person.websites[*].url. Важное примечание: поддерживается только один подстановочный знак на путь. Пример. Предположим, что у нас есть веб-часть со свойствами, соответствующими следующей схеме: { title: string; person: { name: string; bio: string; photoURLs: string[]; websites: { title: string; url: string; }[] } } Мы можем определить метаданные для нужных свойств следующим образом: { 'person.bio': { isRichContent: true }, 'person.photoURLs[*]': { isImageSource: true }, 'person.websites[*].url': { isLink: true } } В результате серверы SharePoint узнают о содержимом свойств и смогут выполнять индексирование поиска, корректировку ссылок и другие операции обработки данных. Если какое-либо из значений потребуется обновить с помощью этих служб, например корректировки ссылок, контейнер свойств веб части обновится автоматически.  |



## <a name="functions"></a>Функции

| Функция     | Возвращаемое значение | Описание |
|:-------------|:------|:---------------|
| [`PropertyPaneButton(targetProperty,properties)`](./sp-webpart-base/propertypanebutton.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneButtonProps`](./sp-webpart-base/ipropertypanebuttonprops.md)>  | Вспомогательный метод для создания кнопки в PropertyPane.  |
| [`PropertyPaneCheckbox(targetProperty,properties)`](./sp-webpart-base/propertypanecheckbox.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneCheckboxProps`](./sp-webpart-base/ipropertypanecheckboxprops.md)>  | Вспомогательный метод для создания флажка в PropertyPane.  |
| [`PropertyPaneChoiceGroup(targetProperty,properties)`](./sp-webpart-base/propertypanechoicegroup.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneChoiceGroupProps`](./sp-webpart-base/ipropertypanechoicegroupprops.md)>  | Вспомогательный метод для создания группы выбора в PropertyPane.  |
| [`PropertyPaneDropdown(targetProperty,properties)`](./sp-webpart-base/propertypanedropdown.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneDropdownProps`](./sp-webpart-base/ipropertypanedropdownprops.md)>  | Вспомогательный метод для создания раскрывающегося меню в PropertyPane.  |
| [`PropertyPaneHorizontalRule(properties)`](./sp-webpart-base/propertypanehorizontalrule.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<void>  | Вспомогательный метод для создания горизонтальной линейки в PropertyPane.  |
| [`PropertyPaneLabel(targetProperty,properties)`](./sp-webpart-base/propertypanelabel.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneLabelProps`](./sp-webpart-base/ipropertypanelabelprops.md)>  | Вспомогательный метод для создания подписи в PropertyPane.  |
| [`PropertyPaneLink(targetProperty,properties)`](./sp-webpart-base/propertypanelink.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneLinkProps`](./sp-webpart-base/ipropertypanelinkprops.md)>  | Вспомогательный метод для создания ссылки в PropertyPane.  |
| [`PropertyPaneSlider(targetProperty,properties)`](./sp-webpart-base/propertypaneslider.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneSliderProps`](./sp-webpart-base/ipropertypanesliderprops.md)>  | Вспомогательный метод для создания ползунка в PropertyPane.  |
| [`PropertyPaneTextField(targetProperty,properties)`](./sp-webpart-base/propertypanetextfield.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneTextFieldProps`](./sp-webpart-base/ipropertypanetextfieldprops.md)>  | Вспомогательный метод для создания текстового поля в PropertyPane.  |
| [`PropertyPaneToggle(targetProperty,properties)`](./sp-webpart-base/propertypanetoggle.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneToggleProps`](./sp-webpart-base/ipropertypanetoggleprops.md)>  | Вспомогательный метод для создания переключателя в PropertyPane.  |


## <a name="enumerations"></a>Перечисления

| Перечисление      | Описание|
|:-----------|:------------|
|[`PropertyPaneButtonType`](./sp-webpart-base/propertypanebuttontype.md)    | Перечисление всех поддерживаемых типов кнопок. |
|[`PropertyPaneFieldType`](./sp-webpart-base/propertypanefieldtype.md)    | Перечисление всех поддерживаемых типов полей PropertyPane. Имена должны соответствовать именам в office-ui-fabric-react. Проверьте регистр букв. |




