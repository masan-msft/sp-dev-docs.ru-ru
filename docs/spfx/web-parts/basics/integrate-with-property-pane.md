---
title: "Сделайте клиентскую веб-часть SharePoint настраиваемой"
description: "Настройте дополнительные свойства в веб-части, используя область свойств."
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: cfb2686d46058cd1bf97321c7928576ba96cf875
ms.sourcegitcommit: 1f1044e59d987d878bb8bc403413e3090234ad44
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/11/2018
---
# <a name="make-your-sharepoint-client-side-web-part-configurable"></a>Сделайте клиентскую веб-часть SharePoint настраиваемой

С помощью области свойств пользователи могут настраивать различные свойства веб-части. В статье [Создание первой веб-части](../get-started/build-a-hello-world-web-part.md) рассказывается, как определить область свойств в классе **HelloWorldWebPart**. Свойства для области свойств определяются в параметре **propertyPaneSettings**.

Область свойств содержит страницу, необязательный заголовок и как минимум одну группу. 

- Элементы **pages** позволяют разделять сложные взаимодействия, добавляя их на одну или несколько страниц. Элементы pages содержат элементы header и groups.
- Элементы **header** позволяют определить заголовок области свойств. 
- Элементы **groups** позволяют определить различные разделы или поля для группировки наборов полей в области свойств.  

На представленном ниже рисунке показан пример области свойств в SharePoint.

![Пример области свойств](../../../images/property-pane-example.png)

## <a name="configure-the-property-pane"></a>Настройка области свойств

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
} from '@microsoft/sp-webpart-base';
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

Если свойства определены, к ним можно обращаться из веб-части с помощью переменной **this.properties.[имя-свойства]**. Дополнительные сведения см. в [описании метода render веб-части HelloWorldWebPart](../get-started/build-a-hello-world-web-part.md#web-part-render-method).

## <a name="handle-field-changes"></a>Обработка изменений полей

У области свойств есть два режима взаимодействия:

* Реактивный
* Нереактивный

В реактивном режиме при каждом изменении вызывается соответствующее событие. В этом режиме веб-часть автоматически обновляется с использованием новых значений.

Хотя реактивного режима достаточно для многих сценариев, иногда требуется нереактивное поведение. В нереактивном режиме веб-часть не обновляется автоматически, если пользователь не подтвердит изменения. 

Чтобы включить нереактивный режим, добавьте в веб-часть следующий код:

```ts 
protected get disableReactivePropertyChanges(): boolean { 
  return true; 
}
```

## <a name="custom-property-pane-controls"></a>Пользовательские элементы управления для области свойств

SharePoint Framework содержит набор стандартных элементов управления для области свойств, но иногда нужны дополнительные функции. SharePoint Framework позволяет создать пользовательские элементы управления для добавления необходимой функции. Дополнительные сведения см. в статье [Создание пользовательских элементов управления для области свойств](../guidance/build-custom-property-pane-controls.md).
