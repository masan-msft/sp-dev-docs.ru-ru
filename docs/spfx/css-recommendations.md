---
title: "Рекомендации по работе с CSS в решениях SharePoint Framework"
description: "Используйте CSS, чтобы описать, как должна выглядеть и работать настройка SharePoint Framework."
ms.date: 1/24/2018
ms.prod: sharepoint
ms.openlocfilehash: 38d74b4a84187b16a3085354a6dda19b60e2eb56
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="recommendations-for-working-with-css-in-sharepoint-framework-solutions"></a><span data-ttu-id="a09af-103">Рекомендации по работе с CSS в решениях SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="a09af-103">Recommendations for working with CSS in SharePoint Framework solutions</span></span>

<span data-ttu-id="a09af-104">Вы можете использовать CSS, чтобы описать, как должна выглядеть и работать настройка SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="a09af-104">When building SharePoint Framework solutions, you can use CSS to define how your customization should look and behave.</span></span> <span data-ttu-id="a09af-105">В этой статье описано, как лучше всего использовать возможности SharePoint Framework и с легкостью создавать стили CSS.</span><span class="sxs-lookup"><span data-stu-id="a09af-105">When building SharePoint Framework solutions, you can use CSS to define how your customization should look like and behave. This article describes how you can make the best use of the capabilities provided with the SharePoint Framework and build your CSS styles in a robust way.</span></span>

## <a name="sharepoint-framework-customizations-are-part-of-the-page"></a><span data-ttu-id="a09af-106">Настройки SharePoint Framework являются частью страницы</span><span class="sxs-lookup"><span data-stu-id="a09af-106">SharePoint Framework customizations are part of the page</span></span>

<span data-ttu-id="a09af-107">Решения SharePoint, созданные по образцу надстройки, изолированы от других элементов на странице.</span><span class="sxs-lookup"><span data-stu-id="a09af-107">When building SharePoint customizations using the add-in model, the solution is isolated from other elements on the page.</span></span> <span data-ttu-id="a09af-108">Код может выполняться в iframe как часть надстройки или как иммерсивное приложение, контролирующее всю страницу.</span><span class="sxs-lookup"><span data-stu-id="a09af-108">Your code can be executed in an iframe as an add-in part, or as an immersive application that takes control of the whole page.</span></span> <span data-ttu-id="a09af-109">В любом случае на него не влияют другие элементы и стили, определенные на странице.</span><span class="sxs-lookup"><span data-stu-id="a09af-109">In both cases, your code is not affected by other elements and styles defined on the page.</span></span>

<span data-ttu-id="a09af-110">Решения SharePoint Framework являются частью страницы и полностью интегрируются с моделью DOM этой страницы.</span><span class="sxs-lookup"><span data-stu-id="a09af-110">SharePoint Framework solutions are a part of the page and integrate fully with the page's DOM.</span></span> <span data-ttu-id="a09af-111">Хотя это снимает ряд ограничений, связанных с моделью надстройки, ваше решение подвергается риску.</span><span class="sxs-lookup"><span data-stu-id="a09af-111">While this removes a number of restrictions that come with the add-in model, it exposes your solution to risk.</span></span> <span data-ttu-id="a09af-112">Если эта часть страницы не будет явно изолирована, к ней будут применяться все стили CSS, которые есть на странице, что может привести к нежелательным результатам.</span><span class="sxs-lookup"><span data-stu-id="a09af-112">Because it's a part of the page, unless explicitly isolated, all CSS styles present on the page apply to it, potentially resulting in an experience different from what you intended.</span></span> <span data-ttu-id="a09af-113">Чтобы избежать таких рисков, нужно определить стили CSS так, чтобы они не влияли ни на что другое на странице, кроме вашей настройки.</span><span class="sxs-lookup"><span data-stu-id="a09af-113">To avoid such risks, you should define your CSS styles in such a way so that they won't affect anything else on the page other than your customization.</span></span>

## <a name="organize-css-files-in-your-solution"></a><span data-ttu-id="a09af-114">Организация файлов CSS в решении</span><span class="sxs-lookup"><span data-stu-id="a09af-114">Organize CSS files in your solution</span></span>

<span data-ttu-id="a09af-115">Пользовательский интерфейс решений часто состоит из нескольких стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="a09af-115">The UI of your solutions often consists of multiple building blocks.</span></span> <span data-ttu-id="a09af-116">Во многих библиотеках JavaScript эти стандартные блоки называются компонентами.</span><span class="sxs-lookup"><span data-stu-id="a09af-116">In many JavaScript libraries, these building blocks are called components.</span></span> <span data-ttu-id="a09af-117">Компонент может быть простым и определять только представление или сложным и включать состояние и другие компоненты.</span><span class="sxs-lookup"><span data-stu-id="a09af-117">A component can be simple and define only the presentation, or it can be more complex and include state and other components.</span></span> <span data-ttu-id="a09af-118">Разделение решения на несколько компонентов позволяет упростить процесс разработки, а также облегчает их тестирование и повторное использование в решении.</span><span class="sxs-lookup"><span data-stu-id="a09af-118">Splitting your solution into multiple components allows you to simplify the development process and makes it easier to test and reuse the components in your solution.</span></span>

<span data-ttu-id="a09af-119">Так как компоненты определяют представление, часто возникает потребность в стилях CSS.</span><span class="sxs-lookup"><span data-stu-id="a09af-119">Because components have presentation, they often require CSS styles.</span></span> <span data-ttu-id="a09af-120">В идеале компоненты должны быть изолированы, чтобы их можно было использовать отдельно.</span><span class="sxs-lookup"><span data-stu-id="a09af-120">Ideally, components should be isolated and be able to be used on their own.</span></span> <span data-ttu-id="a09af-121">Поэтому следует хранить стили CSS для конкретного компонента и все другие файлы ресурсов вместе с компонентом.</span><span class="sxs-lookup"><span data-stu-id="a09af-121">With that in mind, it makes perfect sense for you to store CSS styles for the particular component along with all other asset files next to the component.</span></span> <span data-ttu-id="a09af-122">Ниже приведен пример структуры приложения React с несколькими компонентами вместе с их файлами CSS.</span><span class="sxs-lookup"><span data-stu-id="a09af-122">Following is a sample structure of a React application with a number of components, each with its own CSS file.</span></span>

```text
todoWebPart\components
                      \todoList
                               \todoList.tsx
                               \todoList.module.scss
                      \todoItem
                               \todoItem.tsx
                               \todoItem.module.scss
```

## <a name="use-sass"></a><span data-ttu-id="a09af-123">Использование SASS</span><span class="sxs-lookup"><span data-stu-id="a09af-123">Use Sass</span></span>

<span data-ttu-id="a09af-124">В SharePoint Framework можно использовать как CSS, так и SASS.</span><span class="sxs-lookup"><span data-stu-id="a09af-124">In SharePoint Framework, you can use both CSS and Sass.</span></span> <span data-ttu-id="a09af-125">SASS — это расширенная версия CSS, которая поддерживает переменные, вложение селекторов и примеси — все это упрощает работу со стилями CSS и управление ими в долгосрочной перспективе.</span><span class="sxs-lookup"><span data-stu-id="a09af-125">Sass is a superset of CSS and offers you a number of features such as variables, nesting selectors, or mixins, all of which simplify working with and managing CSS styles over the long term.</span></span> 

<span data-ttu-id="a09af-126">Полный набор функций см. на [веб-сайте Sass](http://sass-lang.com).</span><span class="sxs-lookup"><span data-stu-id="a09af-126">For a complete set of features, see the [Sass website](http://sass-lang.com).</span></span> <span data-ttu-id="a09af-127">Синтаксис CSS полностью совместим с синтаксисом SASS, что очень полезно, если вы еще не работали с SASS раньше и хотите постепенно изучить его возможности.</span><span class="sxs-lookup"><span data-stu-id="a09af-127">All valid CSS is also valid Sass, which is very helpful if you haven't worked with Sass before and want to gradually learn its capabilities.</span></span>

## <a name="avoid-using-ids-in-markup"></a><span data-ttu-id="a09af-128">Не используйте идентификаторы в разметке</span><span class="sxs-lookup"><span data-stu-id="a09af-128">Avoid using ID's in markup</span></span>

<span data-ttu-id="a09af-129">Используя SharePoint Framework, вы создаете настройки, которые пользователи добавляют в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a09af-129">Using SharePoint Framework, you build customizations that end-users add to SharePoint.</span></span> <span data-ttu-id="a09af-130">Невозможно предугадать, сколько экземпляров конкретной настройки будет открыто на странице.</span><span class="sxs-lookup"><span data-stu-id="a09af-130">It's impossible to tell upfront if the particular customization is used only once on a page or if there are multiple instances of it.</span></span> 

<span data-ttu-id="a09af-131">Чтобы избежать проблем, всегда следует предполагать наличие нескольких экземпляров настройки на странице.</span><span class="sxs-lookup"><span data-stu-id="a09af-131">To avoid issues, you should always assume that there are multiple instances of your customization on the same page.</span></span> <span data-ttu-id="a09af-132">Именно поэтому не следует использовать идентификаторы в разметке.</span><span class="sxs-lookup"><span data-stu-id="a09af-132">With that in mind, you should avoid using any IDs in your markup.</span></span> <span data-ttu-id="a09af-133">Идентификаторы на странице должны быть уникальными, а добавление двух одинаковых веб-частей на страницу нарушает это условие и может привести к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="a09af-133">IDs are meant to be unique on a page, and if a user adds your web part to the page twice, it violates this premise, possibly leading to errors.</span></span>

#### <a name="bad-practice"></a><span data-ttu-id="a09af-134">Не рекомендуется</span><span class="sxs-lookup"><span data-stu-id="a09af-134">Bad practice:</span></span>

```typescript
// ...

export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {

  public render(): void {
    this.domElement.innerHTML = `
      <div id="helloWorld">
        Hello world
      </div>`;
  }

  // ...
}
```

<br/>

#### <a name="good-practice"></a><span data-ttu-id="a09af-135">Рекомендуется</span><span class="sxs-lookup"><span data-stu-id="a09af-135">Good practice:</span></span>

```typescript
// ...

export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {

  public render(): void {
    this.domElement.innerHTML = `
      <div class="${styles.helloWorld}">
        Hello world
      </div>`;
  }

  // ...
}
```

## <a name="use-css-modules-to-avoid-styling-conflicts"></a><span data-ttu-id="a09af-136">Использование CSS-модулей для избежания конфликтов стилей</span><span class="sxs-lookup"><span data-stu-id="a09af-136">Use CSS modules to avoid styling conflicts</span></span>

<span data-ttu-id="a09af-p110">Решения SharePoint Framework являются частью страницы. Чтобы стили CSS для одного компонента не влияли на другие элементы на странице, нужно определить селекторы CSS таким образом, чтобы они применялись только к модели DOM вашего решения. Делать это вручную утомительно и потенциально подвержено ошибкам, но SharePoint Framework может сделать это для вас автоматически.</span><span class="sxs-lookup"><span data-stu-id="a09af-p110">SharePoint Framework solutions are a part of the page. To ensure that CSS styles for one component don't affect other elements on the page, you should define your CSS selectors in such a way that they apply only to the DOM of your solution. It's tedious and error-prone to do this manually, but SharePoint Framework can do this automatically for you.</span></span>

<span data-ttu-id="a09af-140">Чтобы избежать конфликтов стилей, SharePoint Framework использует [модули CSS](https://github.com/css-modules/css-modules).</span><span class="sxs-lookup"><span data-stu-id="a09af-140">To help you avoid styling conflicts, SharePoint Framework uses [CSS modules](https://github.com/css-modules/css-modules).</span></span> <span data-ttu-id="a09af-141">При сборке проекта цепочка инструментов SharePoint Framework обрабатывает все файлы с расширением **.module.scss**.</span><span class="sxs-lookup"><span data-stu-id="a09af-141">When building the project, the SharePoint Framework toolchain processes all files with the **.module.scss** extension.</span></span> <span data-ttu-id="a09af-142">Для каждого файла SharePoint Framework считывает все селекторы классов и добавляет к ним уникальное хэш-значение.</span><span class="sxs-lookup"><span data-stu-id="a09af-142">For each file, it reads all class selectors and appends a unique hash value to them.</span></span> <span data-ttu-id="a09af-143">После этого он записывает обновленные селекторы в промежуточные файлы CSS, которые включаются в пакет веб-части.</span><span class="sxs-lookup"><span data-stu-id="a09af-143">After it's finished, it writes the updated selectors to intermediate CSS files that are included in the generated web part bundle.</span></span>

<span data-ttu-id="a09af-144">В продолжение предыдущего примера, предположим, что у вас было два следующих файла SASS:</span><span class="sxs-lookup"><span data-stu-id="a09af-144">Following the example above, assume you had the following two Sass files:</span></span>

#### <a name="todolistmodulescss"></a><span data-ttu-id="a09af-145">todoList.module.scss</span><span class="sxs-lookup"><span data-stu-id="a09af-145">todoList.module.scss:</span></span>

```scss
.todoList {
  margin: 1em 0;

  .text {
    font-weight: bold;
    font-size: 1.5em;
  }
}
```

<br/>

#### <a name="todoitemmodulescss"></a><span data-ttu-id="a09af-146">todoItem.module.scss</span><span class="sxs-lookup"><span data-stu-id="a09af-146">todoItem.module.scss:</span></span>

```scss
.todoItem {
  padding: 0.5em 1em;

  .text {
    font-size: 0.9em;
  }
}
```

<br/>

<span data-ttu-id="a09af-147">После создания проекта в папке **lib** появится два созданных файла CSS, представленных ниже (разрывы строк и отступы добавлены для лучшей читаемости):</span><span class="sxs-lookup"><span data-stu-id="a09af-147">After building the project, in the **lib** folder you would see the following two CSS files generated (line breaks and indenting added for readability):</span></span>

#### <a name="todolistmodulecss"></a><span data-ttu-id="a09af-148">todoList.module.css</span><span class="sxs-lookup"><span data-stu-id="a09af-148">todoList.module.css:</span></span>

```css
.todoList_3e9d35f0 {
  margin:1em 0
}

.todoList_3e9d35f0 .text_3e9d35f0 {
  font-weight:700;
  font-size:1.5em
}
```

<br/>

#### <a name="todoitemmodulecss"></a><span data-ttu-id="a09af-149">todoItem.module.css</span><span class="sxs-lookup"><span data-stu-id="a09af-149">todoItem.module.css:</span></span>

```css
.todoItem_f7081cc4 {
  padding:.5em 1em
}

.todoItem_f7081cc4 .text_f7081cc4 {
  font-size:.9em
}
```

<br/>

<span data-ttu-id="a09af-150">Несмотря на то что в обоих файлах SASS был определен класс **.text**, в созданных файлах CSS к нему добавлены к нему два разных хэша, что делает его уникальным именем класса, характерным для каждого компонента.</span><span class="sxs-lookup"><span data-stu-id="a09af-150">Even though there was a **.text** class defined in both Sass files, notice how in the generated CSS files it has two different hashes appended to it, becoming a unique class name specific to each component.</span></span>

<span data-ttu-id="a09af-p112">Имена классов CSS в модулях CSS генерируются динамически, что делает невозможным непосредственное обращение к ним в коде. Вместо этого при обработке модулей CSS цепочка инструментов SharePoint Framework генерирует файл JavaScript со ссылками на сгенерированные имена классов.</span><span class="sxs-lookup"><span data-stu-id="a09af-p112">The CSS class names in CSS modules are generated dynamically, which makes it impossible for you to refer to them in your code directly. Instead, when processing CSS modules, the SharePoint Framework toolchain generates a JavaScript file with references to the generated class names.</span></span>

#### <a name="todolistmodulescssjs"></a><span data-ttu-id="a09af-153">todoList.module.scss.js</span><span class="sxs-lookup"><span data-stu-id="a09af-153">todoList.module.scss.js:</span></span>

```js
"use strict";
Object.defineProperty(exports, "__esModule", { value: true });
/* tslint:disable */
require('./todoList.module.css');
var styles = {
    todoList: 'todoList_3e9d35f0',
    text: 'text_3e9d35f0',
};
exports.default = styles;
/* tslint:enable */

//# sourceMappingURL=todoList.module.scss.js.map
```

<br/>

<span data-ttu-id="a09af-154">Чтобы использовать сгенерированные имена классов в своем коде, сначала импортируйте стили своего компонента, а затем используйте свойство, указывающее на конкретный класс:</span><span class="sxs-lookup"><span data-stu-id="a09af-154">To use the generated class names in your code, you first import the styles of your component and then use the property pointing to the particular class:</span></span>

```typescript
import styles from './todoList.module.scss';
// ...

export default class TodoList extends React.Component<ITodoListProps, void> {
  public render(): React.ReactElement<ITodoListProps> {
    return (
      <div className={styles.todoList}>
        <div className={styles.text}>Hello world</div>
      </div>
    );
  }
}
```

<br/>

<span data-ttu-id="a09af-155">Для правильной работы модулей CSS должны выполняться следующие условия:</span><span class="sxs-lookup"><span data-stu-id="a09af-155">For the CSS modules to work correctly you have to meet the following conditions:</span></span>

* <span data-ttu-id="a09af-156">Файлы SASS должны иметь расширение **.module.scss**.</span><span class="sxs-lookup"><span data-stu-id="a09af-156">Your Sass files must have the **.module.scss** extension.</span></span> <span data-ttu-id="a09af-157">Если используется расширение **.scss** без **.module**, в ходе сборки отобразится предупреждение.</span><span class="sxs-lookup"><span data-stu-id="a09af-157">If you use the **.scss** extension without **.module**, you see a warning in the build process.</span></span> <span data-ttu-id="a09af-158">Файл SASS будет транспилирован в промежуточный файл CSS, но имена классов *не будут уникальными*.</span><span class="sxs-lookup"><span data-stu-id="a09af-158">The Sass file is transpiled to an intermediate CSS file, but the class names *will not be made unique*.</span></span> <span data-ttu-id="a09af-159">Расширение .module может не использоваться преднамеренно, когда необходимо переопределить сторонние стили CSS.</span><span class="sxs-lookup"><span data-stu-id="a09af-159">In cases when you need to override third-party CSS styles, this might be intended.</span></span>

* <span data-ttu-id="a09af-160">Имена классов CSS должны быть действительными именами переменных JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a09af-160">Your CSS class names must be valid JavaScript variable names.</span></span> <span data-ttu-id="a09af-161">Например, они не могут содержать дефисы: `todoList` — правильно, а `todo-list` — неправильно.</span><span class="sxs-lookup"><span data-stu-id="a09af-161">For example, they cannot contain hyphens: `todoList` is correct, but `todo-list` isn't.</span></span>

* <span data-ttu-id="a09af-162">Рекомендуем указывать имена классов в верблюжьем регистре, но это не обязательно.</span><span class="sxs-lookup"><span data-stu-id="a09af-162">camelCase naming for classes is recommended, but it's not enforced</span></span>

## <a name="wrap-your-css-styles-in-a-class-named-after-the-component"></a><span data-ttu-id="a09af-163">Упаковка стилей CSS в класс, названный именем компонента</span><span class="sxs-lookup"><span data-stu-id="a09af-163">Wrap your CSS styles in a class named after the component</span></span>

<span data-ttu-id="a09af-164">Объединив модули CSS с поддержкой вложения наборов правил SASS, можно упростить стили CSS и убедиться, что они не повлияют на другие элементы на странице.</span><span class="sxs-lookup"><span data-stu-id="a09af-164">By combining CSS modules with Sass' support for nesting rule sets you can simplify your CSS styles and ensure that they won't affect other elements on the page.</span></span>

<span data-ttu-id="a09af-165">Упакуйте стили CSS в класс, названный именем компонента, для которого они созданы.</span><span class="sxs-lookup"><span data-stu-id="a09af-165">When building CSS styles for a component, wrap them in a class named after the component. Then, in the component, assign that class to the component's root element.</span></span> <span data-ttu-id="a09af-166">Затем назначьте этот класс корневому элементу компонента.</span><span class="sxs-lookup"><span data-stu-id="a09af-166">In the component, assign that class to the component's root element.</span></span>

#### <a name="todolistmodulescss"></a><span data-ttu-id="a09af-167">todoList.module.scss</span><span class="sxs-lookup"><span data-stu-id="a09af-167">todoList.module.scss:</span></span>

```scss
.todoList {
  a {
    display: block;
  }
}
```

<br/>

#### <a name="todolisttsx"></a><span data-ttu-id="a09af-168">TodoList.tsx</span><span class="sxs-lookup"><span data-stu-id="a09af-168">TodoList.tsx:</span></span>

```tsx
// ...

export default class TodoList extends React.Component<ITodoListProps, void> {
  public render(): React.ReactElement<ITodoListProps> {
    return (
      <div className={styles.todoList}>
        ...
      </div>
    );
  }
}
```

<br/>

<span data-ttu-id="a09af-169">После транспиляции файл CSS будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="a09af-169">After transpilation, the generated CSS file will look similar to:</span></span>

```css
.todoList_3e9d35f0 a {
  display: block;
}
```

<span data-ttu-id="a09af-170">Так как селектор начинается с уникального имени класса, используемого для компонента, альтернативное представление применяется только к гиперссылкам внутри компонента.</span><span class="sxs-lookup"><span data-stu-id="a09af-170">Because the selector begins with the unique class name, specific to your component, the alternative presentation will apply only to hyperlinks inside your component.</span></span>

## <a name="handling-of-css-vendor-prefix"></a><span data-ttu-id="a09af-171">Обработка префикса поставщика CSS</span><span class="sxs-lookup"><span data-stu-id="a09af-171">Handling of CSS vendor prefix</span></span>

<span data-ttu-id="a09af-172">В SharePoint Framework не требуются свойства стиля с префиксом поставщика в SASS- и CSS-файлах проекта.</span><span class="sxs-lookup"><span data-stu-id="a09af-172">In SPFx no vendor prefixed style properties are required in the SASS or CSS files of a project.</span></span> <span data-ttu-id="a09af-173">Если в поддерживаемых браузерах требуются префиксы, они добавляются после компиляции SASS в CSS автоматически.</span><span class="sxs-lookup"><span data-stu-id="a09af-173">If some of the SPFx supported browsers require prefixes they were added after the SASS to CSS compilation automatically.</span></span> <span data-ttu-id="a09af-174">Этот способ также называется автоматическим добавлением префикса и является фундаментальной составляющей цепочки сборки CSS в SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="a09af-174">This method is also known as auto-prefixing and is a fundamental part of the CSS build chain in SPFx.</span></span>

<span data-ttu-id="a09af-175">Если веб-часть должна использовать новую модель адаптируемого блока (определяется объявлением `display: flex`), в некоторых старых браузерах на основе WebKit и Internet Explorer требуется определенный префикс поставщика в CSS.</span><span class="sxs-lookup"><span data-stu-id="a09af-175">In case a web part should use the new flex box model defined by the `display: flex` declaration, some older WebKit-based and Internet Explorer versions require a particular vendor prefix defined in the CSS.</span></span>

```css
.container{
  display: flex;
}
```

<br/>

<span data-ttu-id="a09af-176">В код SASS артефакта SharePoint не требуется включать префиксы поставщиков.</span><span class="sxs-lookup"><span data-stu-id="a09af-176">In the SASS code of the SPFx artefact does not need to have vendor prefixes included.</span></span> <span data-ttu-id="a09af-177">Они автоматически добавляются после компиляции SASS в CSS. В итоге получается приведенное ниже объявление CSS.</span><span class="sxs-lookup"><span data-stu-id="a09af-177">After the SASS-to-CSS compilation, those were added automatically resulting in the following CSS declaration.</span></span>

```css
.container_7e976ae1 {
  display: -webkit-box; // older Safari on MacOS and iOS
  display: -ms-flexbox; // IE 10 - 11
  display: flex;
}
```

<br/>

<span data-ttu-id="a09af-178">Удаление уже примененных префиксов не только делает код артефакта проще. Это также делает код более легким для чтения и упрощает его использование в будущем.</span><span class="sxs-lookup"><span data-stu-id="a09af-178">Removing already applied prefixes does not only make the code of the artefact cleaner, it also makes it easier to read and future-ready.</span></span> <span data-ttu-id="a09af-179">Кроме того, этот процесс обеспечивает поддержку только тех браузеров, которые совместимы с SharePoint Framework, и защиту от ошибок.</span><span class="sxs-lookup"><span data-stu-id="a09af-179">This process is also configured to support only SharePoint Framework-supported browsers and makes it more error-safe.</span></span>

<span data-ttu-id="a09af-180">Если веб-часть уже содержит префиксы поставщиков в SASS-файлах, которые больше не требуются, этот процесс автоматически удаляет соответствующие объявления.</span><span class="sxs-lookup"><span data-stu-id="a09af-180">In case a web part already has vendor prefixes included in the SASS files that are not needed anymore the same process removes those declarations automatically.</span></span>

<span data-ttu-id="a09af-181">В примере ниже используется свойство `border-radius`, для которого не требуются префиксы поставщиков в поддерживаемых системах.</span><span class="sxs-lookup"><span data-stu-id="a09af-181">The following example makes use of the `border-radius` property, which does not require vendor prefixes on the supported systems.</span></span>

```css
.container {
  /* Safari 3-4, iOS 1-3.2, Android 1.6- */
  -webkit-border-radius: 7px;
  /* Firefox 1-3.6 */
  -moz-border-radius: 7px;
  /* Opera 10.5, IE 9, Safari 5, Chrome, Firefox 4, iOS 4, Android 2.1+ */
  border-radius: 7px;
}
```

<br/>

<span data-ttu-id="a09af-182">Полученная таблица CSS в пакете преобразовывается в приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="a09af-182">The resulting CSS in the package will be converted to the following code.</span></span>

```css
.container_9e54c0b0 {
  border-radius: 7px
}
```

<span data-ttu-id="a09af-183">Дополнительные сведения об автоматическом добавлении префиксов см. в документации из репозитория [autoprefixer](https://github.com/postcss/autoprefixer) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="a09af-183">For more information about auto-prefixing, see the [autoprefixer](https://github.com/postcss/autoprefixer) GitHub repository.</span></span> <span data-ttu-id="a09af-184">База данных с описанием этого процесса доступна на сайте [Can I use__?](https://caniuse.com).</span><span class="sxs-lookup"><span data-stu-id="a09af-184">The database for this process is available on [Can I use__?](https://caniuse.com).</span></span>

## <a name="integrate-office-ui-fabric"></a><span data-ttu-id="a09af-185">Интеграция с Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="a09af-185">Integrate Office UI Fabric</span></span>

<span data-ttu-id="a09af-186">Если ваши настройки будут выглядеть и работать как стандартные функции SharePoint и Office 365, пользователям будет удобнее с ними работать.</span><span class="sxs-lookup"><span data-stu-id="a09af-186">By making your customizations look and behave like the standard functionality of SharePoint and Office 365 you will make it easier for the end-users to work with them.</span></span> <span data-ttu-id="a09af-187">В Office UI Fabric вы найдете набор элементов управления и стилей, при использовании которых ваши настройки будут идеально вписываться в существующий интерфейс.</span><span class="sxs-lookup"><span data-stu-id="a09af-187">Office UI Fabric offers you a set of controls and styles for use in your customizations to seamlessly integrate with the existing user experience.</span></span> 

<span data-ttu-id="a09af-188">Дополнительные сведения об использовании Office UI Fabric в SharePoint Framework см. в [этой статье](./office-ui-fabric-integration.md).</span><span class="sxs-lookup"><span data-stu-id="a09af-188">For more information about using Office UI Fabric in SharePoint Framework, see [Using Office UI Fabric Core and Fabric React in SharePoint Framework](./office-ui-fabric-integration.md).</span></span>

## <a name="use-theme-colors"></a><span data-ttu-id="a09af-189">Использование цветов темы</span><span class="sxs-lookup"><span data-stu-id="a09af-189">Use theme colors</span></span>

<span data-ttu-id="a09af-190">SharePoint позволяет пользователям выбирать цвет темы для своих сайтов.</span><span class="sxs-lookup"><span data-stu-id="a09af-190">SharePoint allows users to choose the theme color for their sites.</span></span> <span data-ttu-id="a09af-191">Тема настройки SharePoint Framework должна соответствовать теме, выбранной пользователями, чтобы настройка выглядела как неотъемлемая часть сайта и излишне не выделялась.</span><span class="sxs-lookup"><span data-stu-id="a09af-191">In your SharePoint Framework customizations, you should follow the theme selected by the users to make your customization look like an integral part of the site rather than unnecessarily stand out.</span></span> 

<span data-ttu-id="a09af-192">Так как пользователи выбирают тему на своем сайте, невозможно предугадать, какие цвета вам следует использовать в настройках, но SharePoint Framework может динамично загружать активную цветовую схему автоматически.</span><span class="sxs-lookup"><span data-stu-id="a09af-192">Because the theme is set by users on their site, you cannot tell upfront which colors your customization should use, but SharePoint Framework can dynamically load the currently active color scheme automatically for you.</span></span> 

<span data-ttu-id="a09af-193">Дополнительные сведения об этой возможности см. в статье [Использование цветов темы в настройках SharePoint Framework](./use-theme-colors-in-your-customizations.md).</span><span class="sxs-lookup"><span data-stu-id="a09af-193">For more information about this capability, see [Use theme colors in your SharePoint Framework customizations](./use-theme-colors-in-your-customizations.md).</span></span>




