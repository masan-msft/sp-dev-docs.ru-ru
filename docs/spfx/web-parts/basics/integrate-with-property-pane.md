---
title: "Сделайте клиентскую веб-часть SharePoint настраиваемой"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 5b63efd205dc55cf741628ecf00bff44efb4c9d1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="make-your-sharepoint-client-side-web-part-configurable"></a>Сделайте клиентскую веб-часть SharePoint настраиваемой

С помощью области свойств пользователи могут настраивать различные свойства веб-части. В статье [Создание первой веб-части](../get-started/build-a-hello-world-web-part.md) рассказывается, как определить область свойств в классе **HelloWorldWebPart**. Свойства для области свойств определяются в параметре **propertyPaneSettings**.

На представленном ниже рисунке показан пример области свойств в SharePoint.

![Пример области свойств](../../../images/property-pane-example.png)

Область свойств содержит метаданные трех основных типов:

* Страницы
* Заголовок
* Группы

Вы можете разделять сложные взаимодействия на страницы. Страницы содержат заголовки и группы.

С помощью заголовка можно определить название области свойств, а с помощью групп — различные разделы области свойств для группирования наборов полей. 

Область свойств должна содержать страницу, необязательный заголовок и как минимум одну группу.

Затем поля свойств определяются в группе. 

## <a name="using-the-property-pane"></a>Использование области свойств

В приведенном ниже примере кода инициализируется и настраивается область свойств для веб-части. Переопределяется метод **getPropertyPaneConfiguration** и возвращается коллекция страниц области свойств.

```ts
protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
  return {
    pages: [
      {
        header: {
          description: strings.PropertyPaneDescription
        },
        groups: [
          {
            groupName: strings.BasicGroupName,
            groupFields: [
              PropertyPaneTextField('description', {
                label: strings.DescriptionFieldLabel
              })
            ]
          }
        ]
      }
    ]
  };
}
```

### <a name="property-pane-fields"></a>Поля области свойств

Поддерживаемые типы полей представлены ниже.

* Кнопка
* Флажок
* Группа выбора
* Раскрывающийся список
* Горизонтальная линейка
* Метка
* Ссылка
* Ползунок
* Текстовое поле
* Многострочное текстовое поле
* Переключатель
* Пользовательский сервер

Типы полей доступны в виде модулей в **sp-client-platform**. Прежде чем использовать их в коде, их необходимо импортировать.

```ts
import {
  PropertyPaneTextField,
  PropertyPaneCheckbox,
  PropertyPaneLabel,
  PropertyPaneLink,
  PropertyPaneSlider,
  PropertyPaneToggle,
  PropertyPaneDropdown
} from '@microsoft/sp-client-preview';
```

Метод определения каждого типа поля приведен ниже (для примера используется тип **PropertyPaneTextField**).

```ts
PropertyPaneTextField('targetProperty',{
  //field properties are defined here
})
```

**targetProperty** определяет объект, связанный с этим типом поля, а также определяется в интерфейсе свойств веб-части.

Чтобы назначить типы этим свойствам, определите в классе веб-части интерфейс, включающий одно или несколько целевых свойств.

```ts
export interface IHelloWorldWebPartProps {
    targetProperty: string
}
```

В веб-части можно получить к нему доступ с помощью свойства **this.properties.targetProperty**.

```ts
<p class="ms-font-l ms-fontColor-white">${this.properties.description}</p>
```

Если свойства определены, к ним можно обращаться из веб-части с помощью переменной **this.properties.[property-name]**. Дополнительные сведения см. в описании метода [**render** веб-части **HelloWorldWebPart**](../get-started/build-a-hello-world-web-part.md#web-part-render-method).

## <a name="handling-field-changes"></a>Обработка изменений полей

У области свойств есть два режима взаимодействия:

* Реактивный
* Нереактивный

В реактивном режиме при каждом изменении вызывается соответствующее событие. В этом режиме веб-часть автоматически обновляется с использованием новых значений.

Хотя реактивного режима достаточно для многих сценариев, иногда требуется нереактивное поведение. В нереактивном режиме веб-часть не обновляется автоматически, если пользователь не подтвердит изменения. Чтобы включить нереактивный режим, добавьте следующий код в веб-часть:

```ts 
protected get disableReactivePropertyChanges(): boolean { 
  return true; 
}
```

## <a name="custom-property-pane-controls"></a>Пользовательский элемент управления области свойств

Платформа SharePoint Framework содержит набор стандартных элементов управления для области свойств, но иногда нужны дополнительные функции. SharePoint Framework дает возможность создавать пользовательские элементы управления для обеспечения требуемой функциональности. Дополнительные сведения см. в руководстве [Создание пользовательских элементов управления для панели свойств](../guidance/build-custom-property-pane-controls.md).
