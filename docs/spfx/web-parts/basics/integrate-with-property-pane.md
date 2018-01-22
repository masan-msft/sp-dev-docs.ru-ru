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
# <a name="make-your-sharepoint-client-side-web-part-configurable"></a><span data-ttu-id="c14ec-103">Сделайте клиентскую веб-часть SharePoint настраиваемой</span><span class="sxs-lookup"><span data-stu-id="c14ec-103">Make your SharePoint client-side web part configurable</span></span>

<span data-ttu-id="c14ec-104">С помощью области свойств пользователи могут настраивать различные свойства веб-части.</span><span class="sxs-lookup"><span data-stu-id="c14ec-104">The property pane allows end users to configure the web part with several properties.</span></span> <span data-ttu-id="c14ec-105">В статье [Создание первой веб-части](../get-started/build-a-hello-world-web-part.md) рассказывается, как определить область свойств в классе **HelloWorldWebPart**.</span><span class="sxs-lookup"><span data-stu-id="c14ec-105">The property pane allows end users to configure the web part with a bunch of properties. The article [Build your first web part](../get-started/build-a-hello-world-web-part.md) describes how the property pane is defined in the **HelloWorldWebPart** class. The property pane properties are defined in  propertyPaneSettings.</span></span> <span data-ttu-id="c14ec-106">Свойства для области свойств определяются в параметре **propertyPaneSettings**.</span><span class="sxs-lookup"><span data-stu-id="c14ec-106">The property pane properties are defined in **propertyPaneSettings**.</span></span>

<span data-ttu-id="c14ec-107">Область свойств содержит страницу, необязательный заголовок и как минимум одну группу.</span><span class="sxs-lookup"><span data-stu-id="c14ec-107">A property pane should contain a page, an optional header, and at least one group.</span></span> 

- <span data-ttu-id="c14ec-108">Элементы **pages** позволяют разделять сложные взаимодействия, добавляя их на одну или несколько страниц.</span><span class="sxs-lookup"><span data-stu-id="c14ec-108">Pages provide you the flexibility to separate complex interactions and put them into one or more pages. Pages then contain Header and Groups.</span></span> <span data-ttu-id="c14ec-109">Элементы pages содержат элементы header и groups.</span><span class="sxs-lookup"><span data-stu-id="c14ec-109">Pages contain a header and groups.</span></span>
- <span data-ttu-id="c14ec-110">Элементы **header** позволяют определить заголовок области свойств.</span><span class="sxs-lookup"><span data-stu-id="c14ec-110">**Headers** allow you to define the title of the property pane.</span></span> 
- <span data-ttu-id="c14ec-111">Элементы **groups** позволяют определить различные разделы или поля для группировки наборов полей в области свойств.</span><span class="sxs-lookup"><span data-stu-id="c14ec-111">Header allows you to define the title of the property pane and Groups let you define the various sections for the property pane through which you want to group your field sets.</span></span>  

<span data-ttu-id="c14ec-112">На представленном ниже рисунке показан пример области свойств в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c14ec-112">The following figure shows an example of a property pane in SharePoint.</span></span>

![Пример области свойств](../../../images/property-pane-example.png)

## <a name="configure-the-property-pane"></a><span data-ttu-id="c14ec-114">Настройка области свойств</span><span class="sxs-lookup"><span data-stu-id="c14ec-114">Configure the Web part property pane</span></span>

<span data-ttu-id="c14ec-p103">В приведенном ниже примере кода инициализируется и настраивается область свойств для веб-части. Переопределяется метод **getPropertyPaneConfiguration** и возвращается коллекция страниц области свойств.</span><span class="sxs-lookup"><span data-stu-id="c14ec-p103">The following code example initializes and configures the property pane in your web part. You override the **getPropertyPaneConfiguration** method and return a collection of property pane page(s).</span></span>

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

### <a name="property-pane-fields"></a><span data-ttu-id="c14ec-117">Поля области свойств</span><span class="sxs-lookup"><span data-stu-id="c14ec-117">Property pane fields</span></span>

<span data-ttu-id="c14ec-118">Поддерживаемые типы полей представлены ниже.</span><span class="sxs-lookup"><span data-stu-id="c14ec-118">The following field types are supported:</span></span>

* <span data-ttu-id="c14ec-119">Кнопка</span><span class="sxs-lookup"><span data-stu-id="c14ec-119">Button</span></span>
* <span data-ttu-id="c14ec-120">Флажок</span><span class="sxs-lookup"><span data-stu-id="c14ec-120">Checkbox</span></span>
* <span data-ttu-id="c14ec-121">Группа выбора</span><span class="sxs-lookup"><span data-stu-id="c14ec-121">Choice group</span></span>
* <span data-ttu-id="c14ec-122">Раскрывающийся список</span><span class="sxs-lookup"><span data-stu-id="c14ec-122">Dropdown</span></span>
* <span data-ttu-id="c14ec-123">Горизонтальная линейка</span><span class="sxs-lookup"><span data-stu-id="c14ec-123">Horizontal rule</span></span>
* <span data-ttu-id="c14ec-124">Метка</span><span class="sxs-lookup"><span data-stu-id="c14ec-124">Label</span></span>
* <span data-ttu-id="c14ec-125">Ссылка</span><span class="sxs-lookup"><span data-stu-id="c14ec-125">Link</span></span>
* <span data-ttu-id="c14ec-126">Ползунок</span><span class="sxs-lookup"><span data-stu-id="c14ec-126">Slider</span></span>
* <span data-ttu-id="c14ec-127">Текстовое поле</span><span class="sxs-lookup"><span data-stu-id="c14ec-127">Textbox</span></span>
* <span data-ttu-id="c14ec-128">Многострочное текстовое поле</span><span class="sxs-lookup"><span data-stu-id="c14ec-128">Multi-line Textbox</span></span>
* <span data-ttu-id="c14ec-129">Переключатель</span><span class="sxs-lookup"><span data-stu-id="c14ec-129">Toggle</span></span>
* <span data-ttu-id="c14ec-130">Пользовательский сервер</span><span class="sxs-lookup"><span data-stu-id="c14ec-130">Custom</span></span>

<span data-ttu-id="c14ec-p104">Типы полей доступны в виде модулей в **sp-client-platform**. Прежде чем использовать их в коде, их необходимо импортировать.</span><span class="sxs-lookup"><span data-stu-id="c14ec-p104">The field types are available as modules in **sp-client-platform**. They require an import before you can use them in your code:</span></span>

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

<span data-ttu-id="c14ec-133">Метод определения каждого типа поля приведен ниже (для примера используется тип **PropertyPaneTextField**).</span><span class="sxs-lookup"><span data-stu-id="c14ec-133">Every field type method is defined as follows, taking **PropertyPaneTextField** as an example:</span></span>

```ts
PropertyPaneTextField('targetProperty',{
  //field properties are defined here
})
```

<span data-ttu-id="c14ec-134">**targetProperty** определяет объект, связанный с этим типом поля, а также определяется в интерфейсе свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="c14ec-134">**targetProperty** defines the associated object for that field type and is also defined in the props interface in your web part.</span></span>

<span data-ttu-id="c14ec-135">Чтобы назначить типы этим свойствам, определите в классе веб-части интерфейс, включающий одно или несколько целевых свойств.</span><span class="sxs-lookup"><span data-stu-id="c14ec-135">To assign types to these properties, define an interface in your web part class that includes one or more target properties.</span></span>

```ts
export interface IHelloWorldWebPartProps {
    targetProperty: string
}
```

<span data-ttu-id="c14ec-136">В веб-части можно получить к нему доступ с помощью свойства **this.properties.targetProperty**.</span><span class="sxs-lookup"><span data-stu-id="c14ec-136">This is then available in your web part using **this.properties.targetProperty**.</span></span>

```ts
<p class="ms-font-l ms-fontColor-white">${this.properties.description}</p>
```

<span data-ttu-id="c14ec-137">Если свойства определены, к ним можно обращаться из веб-части с помощью переменной **this.properties.[имя-свойства]**.</span><span class="sxs-lookup"><span data-stu-id="c14ec-137">When the properties are defined, you can access them in your web part using the **this.properties.[property-name]**. For details, see render method of the HelloWorldWebPart.</span></span> <span data-ttu-id="c14ec-138">Дополнительные сведения см. в [описании метода render веб-части HelloWorldWebPart](../get-started/build-a-hello-world-web-part.md#web-part-render-method).</span><span class="sxs-lookup"><span data-stu-id="c14ec-138">For more information, see [render method of the HelloWorldWebPart](../get-started/build-a-hello-world-web-part.md#web-part-render-method).</span></span>

## <a name="handle-field-changes"></a><span data-ttu-id="c14ec-139">Обработка изменений полей</span><span class="sxs-lookup"><span data-stu-id="c14ec-139">Handle field changes</span></span>

<span data-ttu-id="c14ec-140">У области свойств есть два режима взаимодействия:</span><span class="sxs-lookup"><span data-stu-id="c14ec-140">The property pane has two interaction modes:</span></span>

* <span data-ttu-id="c14ec-141">Реактивный</span><span class="sxs-lookup"><span data-stu-id="c14ec-141">Reactive</span></span>
* <span data-ttu-id="c14ec-142">Нереактивный</span><span class="sxs-lookup"><span data-stu-id="c14ec-142">Non-reactive</span></span>

<span data-ttu-id="c14ec-p106">В реактивном режиме при каждом изменении вызывается соответствующее событие. В этом режиме веб-часть автоматически обновляется с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="c14ec-p106">In reactive mode, on every change, a change event is triggered. Reactive behavior automatically updates the web part with the new values.</span></span>

<span data-ttu-id="c14ec-145">Хотя реактивного режима достаточно для многих сценариев, иногда требуется нереактивное поведение.</span><span class="sxs-lookup"><span data-stu-id="c14ec-145">While reactive mode is sufficient for many scenarios, at times you will need non-reactive behavior. Non-reactive does not update the web part automatically unless the user confirms the changes.</span></span> <span data-ttu-id="c14ec-146">В нереактивном режиме веб-часть не обновляется автоматически, если пользователь не подтвердит изменения.</span><span class="sxs-lookup"><span data-stu-id="c14ec-146">While reactive mode is sufficient for many scenarios, at times you will need non-reactive behavior. Non-reactive does not update the web part automatically unless the user confirms the changes.</span></span> 

<span data-ttu-id="c14ec-147">Чтобы включить нереактивный режим, добавьте в веб-часть следующий код:</span><span class="sxs-lookup"><span data-stu-id="c14ec-147">To turn on the non-reactive mode, add the following code in your web part:</span></span>

```ts 
protected get disableReactivePropertyChanges(): boolean { 
  return true; 
}
```

## <a name="custom-property-pane-controls"></a><span data-ttu-id="c14ec-148">Пользовательские элементы управления для области свойств</span><span class="sxs-lookup"><span data-stu-id="c14ec-148">Custom property pane controls</span></span>

<span data-ttu-id="c14ec-149">SharePoint Framework содержит набор стандартных элементов управления для области свойств,</span><span class="sxs-lookup"><span data-stu-id="c14ec-149">SharePoint Framework contains a set of standard controls for the property pane.</span></span> <span data-ttu-id="c14ec-150">но иногда нужны дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="c14ec-150">But sometimes you need additional functionality beyond the basic controls.</span></span> <span data-ttu-id="c14ec-151">SharePoint Framework позволяет создать пользовательские элементы управления для добавления необходимой функции.</span><span class="sxs-lookup"><span data-stu-id="c14ec-151">SharePoint Framework allows you to build custom controls to deliver the required functionality.</span></span> <span data-ttu-id="c14ec-152">Дополнительные сведения см. в статье [Создание пользовательских элементов управления для области свойств](../guidance/build-custom-property-pane-controls.md).</span><span class="sxs-lookup"><span data-stu-id="c14ec-152">To learn more, read the [Build custom controls for the property pane](../guidance/build-custom-property-pane-controls.md) guide.</span></span>
