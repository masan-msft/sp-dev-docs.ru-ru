# <a name="integrate-your-sharepoint-client-side-web-part-with-the-property-pane"></a><span data-ttu-id="4dea2-101">Интеграция клиентской веб-части SharePoint с областью задач</span><span class="sxs-lookup"><span data-stu-id="4dea2-101">Integrate your SharePoint client-side web part with the property pane</span></span>

<span data-ttu-id="4dea2-p101">С помощью области свойств пользователи могут настраивать различные свойства веб-части. В статье [Создание первой веб-части](../get-started/build-a-hello-world-web-part) рассказывается, как определить область свойств в классе **HelloWorldWebPart**. Свойства для области свойств определяются в параметре **propertyPaneSettings**.</span><span class="sxs-lookup"><span data-stu-id="4dea2-p101">The property pane allows end users to configure the web part with a bunch of properties. The article [Build your first web part](../get-started/build-a-hello-world-web-part) describes how the property pane is defined in the **HelloWorldWebPart** class. The property pane properties are defined in  **propertyPaneSettings**.</span></span>

<span data-ttu-id="4dea2-105">На представленном ниже рисунке показан пример области свойств в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4dea2-105">The following figure shows an example of a property pane in SharePoint.</span></span>

![Пример области свойств](../../../../images/property-pane-example.png)

<span data-ttu-id="4dea2-107">Область свойств содержит метаданные трех основных типов:</span><span class="sxs-lookup"><span data-stu-id="4dea2-107">The property pane has three key metadata:</span></span>

* <span data-ttu-id="4dea2-108">Страницы</span><span class="sxs-lookup"><span data-stu-id="4dea2-108">Pages</span></span>
* <span data-ttu-id="4dea2-109">Заголовок</span><span class="sxs-lookup"><span data-stu-id="4dea2-109">Header</span></span>
* <span data-ttu-id="4dea2-110">Группы</span><span class="sxs-lookup"><span data-stu-id="4dea2-110">Groups</span></span>

<span data-ttu-id="4dea2-p102">Вы можете разделять сложные взаимодействия на страницы. Страницы содержат заголовки и группы.</span><span class="sxs-lookup"><span data-stu-id="4dea2-p102">Pages provide you the flexibility to separate complex interactions and put them into one or more pages. Pages then contain Header and Groups.</span></span>

<span data-ttu-id="4dea2-113">С помощью заголовка можно определить название области свойств, а с помощью групп — различные разделы области свойств для группирования наборов полей.</span><span class="sxs-lookup"><span data-stu-id="4dea2-113">Header allows you to define the title of the property pane and Groups let you define the various sections for the property pane through which you want to group your field sets.</span></span> 

<span data-ttu-id="4dea2-114">Область свойств должна содержать страницу, необязательный заголовок и как минимум одну группу.</span><span class="sxs-lookup"><span data-stu-id="4dea2-114">A property pane should contain a page, an optional header, and at least one group.</span></span>

<span data-ttu-id="4dea2-115">Затем поля свойств определяются в группе.</span><span class="sxs-lookup"><span data-stu-id="4dea2-115">Property fields are then defined inside a group.</span></span> 

## <a name="using-the-property-pane"></a><span data-ttu-id="4dea2-116">Использование области свойств</span><span class="sxs-lookup"><span data-stu-id="4dea2-116">Using the property pane</span></span>

<span data-ttu-id="4dea2-p103">В приведенном ниже примере кода инициализируется и настраивается область свойств для веб-части. Создается метод типа **IPropertyPaneSettings** и возвращается коллекция страниц области свойств.</span><span class="sxs-lookup"><span data-stu-id="4dea2-p103">The following code example initializes and configures the property pane in your web part. You create a method of type **IPropertyPaneSettings** and return a collection of property pane page(s).</span></span>

```ts
protected get propertyPaneSettings(): IPropertyPaneSettings {
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

### <a name="property-pane-fields"></a><span data-ttu-id="4dea2-119">Поля области свойств</span><span class="sxs-lookup"><span data-stu-id="4dea2-119">Property pane fields</span></span>

<span data-ttu-id="4dea2-120">Поддерживаются следующие типы полей:</span><span class="sxs-lookup"><span data-stu-id="4dea2-120">The following field types are supported:</span></span>

* <span data-ttu-id="4dea2-121">Подпись</span><span class="sxs-lookup"><span data-stu-id="4dea2-121">Label</span></span>
* <span data-ttu-id="4dea2-122">Текстовое поле</span><span class="sxs-lookup"><span data-stu-id="4dea2-122">Textbox</span></span>
* <span data-ttu-id="4dea2-123">Многострочное текстовое поле</span><span class="sxs-lookup"><span data-stu-id="4dea2-123">Multi-line Textbox</span></span>
* <span data-ttu-id="4dea2-124">Флажок</span><span class="sxs-lookup"><span data-stu-id="4dea2-124">Checkbox</span></span>
* <span data-ttu-id="4dea2-125">Раскрывающийся список</span><span class="sxs-lookup"><span data-stu-id="4dea2-125">Dropdown</span></span>
* <span data-ttu-id="4dea2-126">Ссылка</span><span class="sxs-lookup"><span data-stu-id="4dea2-126">Link</span></span>
* <span data-ttu-id="4dea2-127">Ползунок</span><span class="sxs-lookup"><span data-stu-id="4dea2-127">Slider</span></span>
* <span data-ttu-id="4dea2-128">Переключатель</span><span class="sxs-lookup"><span data-stu-id="4dea2-128">Toggle</span></span>
* <span data-ttu-id="4dea2-129">Пользовательский сервер</span><span class="sxs-lookup"><span data-stu-id="4dea2-129">Custom</span></span>

<span data-ttu-id="4dea2-p104">Типы полей доступны в виде модулей в **sp-client-platform**. Прежде чем использовать их в коде, их необходимо импортировать:</span><span class="sxs-lookup"><span data-stu-id="4dea2-p104">The field types are available as modules in **sp-client-platform**. They require an import before you can use them in your code:</span></span>

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

<span data-ttu-id="4dea2-132">Конструктор каждого типа поля определяется следующим образом (для примера используется тип **PropertyPaneTextField**):</span><span class="sxs-lookup"><span data-stu-id="4dea2-132">Every field type constructor is defined as follows, taking **PropertyPaneTextField** as an example:</span></span>

```ts
PropertyPaneTextField('targetProperty',{
  //field properties are defined here
})
```

<span data-ttu-id="4dea2-133">**targetProperty** определяет объект, связанный с этим типом поля, а также определяется в интерфейсе свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="4dea2-133">**targetProperty** defines the associated object for that field type and is also defined in the props interface in your web part.</span></span>

<span data-ttu-id="4dea2-134">Чтобы назначить типы этим свойствам, определите в классе веб-части интерфейс, включающий одно или несколько целевых свойств.</span><span class="sxs-lookup"><span data-stu-id="4dea2-134">To assign types to these properties, define an interface in your web part class that includes one or more target properties.</span></span>

```ts
export interface IHelloWorldWebPartProps {
    targetProperty: string
}
```

<span data-ttu-id="4dea2-135">В веб-части можно получить к нему доступ с помощью свойства **this.properties.targetProperty**.</span><span class="sxs-lookup"><span data-stu-id="4dea2-135">This is then available in your web part using **this.properties.targetProperty**.</span></span>

```ts
<p class="ms-font-l ms-fontColor-white">${this.properties.description}</p>
```

<span data-ttu-id="4dea2-p105">Если свойства определены, к ним можно обращаться из веб-части с помощью переменной **this.properties.<значение_свойства>**. Дополнительные сведения см. в описании метода [**render** веб-части **HelloWorldWebPart**](../get-started/build-a-hello-world-web-part#web-part-render-method):</span><span class="sxs-lookup"><span data-stu-id="4dea2-p105">When the properties are defined, you can access them in your web part using the **this.properties.<property-value>**. For details, see [**render** method of the **HelloWorldWebPart**](../get-started/build-a-hello-world-web-part#web-part-render-method):</span></span>

## <a name="handling-field-changes"></a><span data-ttu-id="4dea2-138">Обработка изменения полей</span><span class="sxs-lookup"><span data-stu-id="4dea2-138">Handling field changes</span></span>

<span data-ttu-id="4dea2-139">У области свойств есть два режима взаимодействия:</span><span class="sxs-lookup"><span data-stu-id="4dea2-139">The property pane has two interaction modes:</span></span>

* <span data-ttu-id="4dea2-140">Реактивный</span><span class="sxs-lookup"><span data-stu-id="4dea2-140">Reactive</span></span>
* <span data-ttu-id="4dea2-141">Нереактивный</span><span class="sxs-lookup"><span data-stu-id="4dea2-141">Non-reactive</span></span>

<span data-ttu-id="4dea2-p106">В реактивном режиме при каждом изменении вызывается соответствующее событие. В этом режиме веб-часть автоматически обновляется с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="4dea2-p106">In reactive mode, on every change, a change event is triggered. Reactive behavior automatically updates the web part with the new values.</span></span>

<span data-ttu-id="4dea2-p107">Хотя реактивного режима достаточно для многих сценариев, иногда требуется нереактивное поведение. В нереактивном режиме веб-часть не обновляется автоматически, если пользователь не подтвердит изменения. Чтобы включить нереактивный режим, добавьте следующий код в веб-часть:</span><span class="sxs-lookup"><span data-stu-id="4dea2-p107">While reactive mode is sufficient for many scenarios, at times you will need non-reactive behavior. Non-reactive does not update the web part automatically unless the user confirms the changes. To turn on the non-reactive mode, add the following code in your web part:</span></span>

```ts 
protected get disableReactivePropertyChanges(): boolean { 
  return true; 
}
```

## <a name="custom-field-example"></a><span data-ttu-id="4dea2-147">Пример настраиваемого поля</span><span class="sxs-lookup"><span data-stu-id="4dea2-147">Custom field example</span></span>

<span data-ttu-id="4dea2-148">Добавьте следующее определение поля в массив **groupFields**:</span><span class="sxs-lookup"><span data-stu-id="4dea2-148">Add the following field definition in a **groupFields** array.</span></span>

```ts
{
  type: IPropertyPaneFieldType.Custom,
  targetProperty: 'custom',
  properties: {
    onRender: this._customFieldRender.bind(this),
    value: undefined,
    context: undefined
  }
}
```

<span data-ttu-id="4dea2-149">Добавьте следующие типы в импортированные элементы **@microsoft/sp-webpart-base**:</span><span class="sxs-lookup"><span data-stu-id="4dea2-149">Add the following types to the **@microsoft/sp-webpart-base** imports.</span></span>

```ts
IPropertyPaneFieldType
```

<span data-ttu-id="4dea2-150">Добавьте следующий частный метод для отрисовки настраиваемого поля:</span><span class="sxs-lookup"><span data-stu-id="4dea2-150">Add the following private method to render the custom field.</span></span>

```ts
private _customFieldRender(elem: HTMLElement, context: any, onChanged?: IOnCustomPropertyFieldChanged): void {
    elem.innerHTML = '<input id="password" type="password" name="password" class="ms-TextField-field">';
}
```
