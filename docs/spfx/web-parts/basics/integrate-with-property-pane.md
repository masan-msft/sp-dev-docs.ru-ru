# <a name="make-your-sharepoint-client-side-web-part-configurable"></a><span data-ttu-id="4ebcb-101">Сделайте клиентскую веб-часть SharePoint настраиваемой</span><span class="sxs-lookup"><span data-stu-id="4ebcb-101">Make your SharePoint client-side web part configurable</span></span>

<span data-ttu-id="4ebcb-p101">С помощью области свойств пользователи могут настраивать различные свойства веб-части. В статье [Создание первой веб-части](../get-started/build-a-hello-world-web-part) рассказывается, как определить область свойств в классе **HelloWorldWebPart**. Свойства для области свойств определяются в параметре **propertyPaneSettings**.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-p101">The property pane allows end users to configure the web part with a bunch of properties. The article [Build your first web part](../get-started/build-a-hello-world-web-part) describes how the property pane is defined in the **HelloWorldWebPart** class. The property pane properties are defined in  **propertyPaneSettings**.</span></span>

<span data-ttu-id="4ebcb-105">На представленном ниже рисунке показан пример области свойств в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-105">The following figure shows an example of a property pane in SharePoint.</span></span>

![Пример области свойств](../../../../images/property-pane-example.png)

<span data-ttu-id="4ebcb-107">Область свойств содержит метаданные трех основных типов:</span><span class="sxs-lookup"><span data-stu-id="4ebcb-107">The property pane has three key metadata:</span></span>

* <span data-ttu-id="4ebcb-108">Страницы</span><span class="sxs-lookup"><span data-stu-id="4ebcb-108">Pages</span></span>
* <span data-ttu-id="4ebcb-109">Заголовок</span><span class="sxs-lookup"><span data-stu-id="4ebcb-109">Header</span></span>
* <span data-ttu-id="4ebcb-110">Группы</span><span class="sxs-lookup"><span data-stu-id="4ebcb-110">Groups</span></span>

<span data-ttu-id="4ebcb-p102">Вы можете разделять сложные взаимодействия на страницы. Страницы содержат заголовки и группы.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-p102">Pages provide you the flexibility to separate complex interactions and put them into one or more pages. Pages then contain Header and Groups.</span></span>

<span data-ttu-id="4ebcb-113">С помощью заголовка можно определить название области свойств, а с помощью групп — различные разделы области свойств для группирования наборов полей.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-113">Header allows you to define the title of the property pane and Groups let you define the various sections for the property pane through which you want to group your field sets.</span></span> 

<span data-ttu-id="4ebcb-114">Область свойств должна содержать страницу, необязательный заголовок и как минимум одну группу.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-114">A property pane should contain a page, an optional header, and at least one group.</span></span>

<span data-ttu-id="4ebcb-115">Затем поля свойств определяются в группе.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-115">Property fields are then defined inside a group.</span></span> 

## <a name="using-the-property-pane"></a><span data-ttu-id="4ebcb-116">Использование области свойств</span><span class="sxs-lookup"><span data-stu-id="4ebcb-116">Using the property pane</span></span>

<span data-ttu-id="4ebcb-p103">В приведенном ниже примере кода инициализируется и настраивается область свойств для веб-части. Переопределяется метод **getPropertyPaneConfiguration** и возвращается коллекция страниц области свойств.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-p103">The following code example initializes and configures the property pane in your web part. You create a method of type **IPropertyPaneSettings** and return a collection of property pane page(s).</span></span>

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

### <a name="property-pane-fields"></a><span data-ttu-id="4ebcb-119">Поля области свойств</span><span class="sxs-lookup"><span data-stu-id="4ebcb-119">Property pane fields</span></span>

<span data-ttu-id="4ebcb-120">Поддерживаемые типы полей представлены ниже.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-120">The following field types are supported:</span></span>

* <span data-ttu-id="4ebcb-121">Кнопка</span><span class="sxs-lookup"><span data-stu-id="4ebcb-121">Button</span></span>
* <span data-ttu-id="4ebcb-122">Флажок</span><span class="sxs-lookup"><span data-stu-id="4ebcb-122">Checkbox</span></span>
* <span data-ttu-id="4ebcb-123">Группа выбора</span><span class="sxs-lookup"><span data-stu-id="4ebcb-123">Choice Group</span></span>
* <span data-ttu-id="4ebcb-124">Раскрывающийся список</span><span class="sxs-lookup"><span data-stu-id="4ebcb-124">Dropdown</span></span>
* <span data-ttu-id="4ebcb-125">Горизонтальная линейка</span><span class="sxs-lookup"><span data-stu-id="4ebcb-125">Horizontal rule</span></span>
* <span data-ttu-id="4ebcb-126">Метка</span><span class="sxs-lookup"><span data-stu-id="4ebcb-126">Label</span></span>
* <span data-ttu-id="4ebcb-127">Ссылка</span><span class="sxs-lookup"><span data-stu-id="4ebcb-127">Link</span></span>
* <span data-ttu-id="4ebcb-128">Ползунок</span><span class="sxs-lookup"><span data-stu-id="4ebcb-128">Slider</span></span>
* <span data-ttu-id="4ebcb-129">Текстовое поле</span><span class="sxs-lookup"><span data-stu-id="4ebcb-129">Textbox</span></span>
* <span data-ttu-id="4ebcb-130">Многострочное текстовое поле</span><span class="sxs-lookup"><span data-stu-id="4ebcb-130">Multi-line Textbox</span></span>
* <span data-ttu-id="4ebcb-131">Переключатель</span><span class="sxs-lookup"><span data-stu-id="4ebcb-131">Toggle</span></span>
* <span data-ttu-id="4ebcb-132">Пользовательский сервер</span><span class="sxs-lookup"><span data-stu-id="4ebcb-132">Custom</span></span>

<span data-ttu-id="4ebcb-p104">Типы полей доступны в виде модулей в **sp-client-platform**. Прежде чем использовать их в коде, их необходимо импортировать.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-p104">The field types are available as modules in **sp-client-platform**. They require an import before you can use them in your code:</span></span>

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

<span data-ttu-id="4ebcb-135">Метод определения каждого типа поля приведен ниже (для примера используется тип **PropertyPaneTextField**).</span><span class="sxs-lookup"><span data-stu-id="4ebcb-135">Every field type constructor is defined as follows, taking **PropertyPaneTextField** as an example:</span></span>

```ts
PropertyPaneTextField('targetProperty',{
  //field properties are defined here
})
```

<span data-ttu-id="4ebcb-136">**targetProperty** определяет объект, связанный с этим типом поля, а также определяется в интерфейсе свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-136">**targetProperty** defines the associated object for that field type and is also defined in the props interface in your web part.</span></span>

<span data-ttu-id="4ebcb-137">Чтобы назначить типы этим свойствам, определите в классе веб-части интерфейс, включающий одно или несколько целевых свойств.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-137">To assign types to these properties, define an interface in your web part class that includes one or more target properties.</span></span>

```ts
export interface IHelloWorldWebPartProps {
    targetProperty: string
}
```

<span data-ttu-id="4ebcb-138">В веб-части можно получить к нему доступ с помощью свойства **this.properties.targetProperty**.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-138">This is then available in your web part using **this.properties.targetProperty**.</span></span>

```ts
<p class="ms-font-l ms-fontColor-white">${this.properties.description}</p>
```

<span data-ttu-id="4ebcb-p105">Если свойства определены, к ним можно обращаться из веб-части с помощью переменной **this.properties.[property-name]**. Дополнительные сведения см. в описании метода [**render** веб-части **HelloWorldWebPart**](../get-started/build-a-hello-world-web-part#web-part-render-method).</span><span class="sxs-lookup"><span data-stu-id="4ebcb-p105">When the properties are defined, you can access them in your web part using the **this.properties.<property-value>**. For details, see [**render** method of the **HelloWorldWebPart**](../get-started/build-a-hello-world-web-part#web-part-render-method):</span></span>

## <a name="handling-field-changes"></a><span data-ttu-id="4ebcb-141">Обработка изменений полей</span><span class="sxs-lookup"><span data-stu-id="4ebcb-141">Handling field changes</span></span>

<span data-ttu-id="4ebcb-142">У области свойств есть два режима взаимодействия:</span><span class="sxs-lookup"><span data-stu-id="4ebcb-142">The property pane has two interaction modes:</span></span>

* <span data-ttu-id="4ebcb-143">Реактивный</span><span class="sxs-lookup"><span data-stu-id="4ebcb-143">Reactive</span></span>
* <span data-ttu-id="4ebcb-144">Нереактивный</span><span class="sxs-lookup"><span data-stu-id="4ebcb-144">Non-reactive</span></span>

<span data-ttu-id="4ebcb-p106">В реактивном режиме при каждом изменении вызывается соответствующее событие. В этом режиме веб-часть автоматически обновляется с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="4ebcb-p106">In reactive mode, on every change, a change event is triggered. Reactive behavior automatically updates the web part with the new values.</span></span>

<span data-ttu-id="4ebcb-p107">Хотя реактивного режима достаточно для многих сценариев, иногда требуется нереактивное поведение. В нереактивном режиме веб-часть не обновляется автоматически, если пользователь не подтвердит изменения. Чтобы включить нереактивный режим, добавьте следующий код в веб-часть:</span><span class="sxs-lookup"><span data-stu-id="4ebcb-p107">While reactive mode is sufficient for many scenarios, at times you will need non-reactive behavior. Non-reactive does not update the web part automatically unless the user confirms the changes. To turn on the non-reactive mode, add the following code in your web part:</span></span>

```ts 
protected get disableReactivePropertyChanges(): boolean { 
  return true; 
}
```

## <a name="custom-property-pane-controls"></a><span data-ttu-id="4ebcb-150">Пользовательский элемент управления области свойств</span><span class="sxs-lookup"><span data-stu-id="4ebcb-150">Custom property pane controls</span></span>

<span data-ttu-id="4ebcb-p108">Платформа SharePoint Framework содержит набор стандартных элементов управления для области свойств, но иногда нужны дополнительные функции. SharePoint Framework дает возможность создавать пользовательские элементы управления для обеспечения требуемой функциональности. Дополнительные сведения см. в руководстве [Создание пользовательских элементов управления для панели свойств](../guidance/build-custom-property-pane-controls).</span><span class="sxs-lookup"><span data-stu-id="4ebcb-p108">SharePoint Framework contains a set of standard controls for the property pane. But sometimes you need additional functionality beyond the basic controls. SharePoint Framework allows you to build custom controls to deliver the require functionality. To learn more, read the [Build custom controls for the property pane](../guidance/build-custom-property-pane-controls) guide.</span></span>