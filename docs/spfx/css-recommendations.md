---
title: "Рекомендации по работе с CSS в решениях SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: c55b5362b4a1426c44cc0e7c53eacfe08982de64
ms.sourcegitcommit: 3276e9b281b227fb2f1a131ab4ac54ae212ce5cf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2017
---
# <a name="recommendations-for-working-with-css-in-sharepoint-framework-solutions"></a><span data-ttu-id="66e05-102">Рекомендации по работе с CSS в решениях SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="66e05-102">Recommendations for working with CSS in SharePoint Framework solutions</span></span>

<span data-ttu-id="66e05-p101">При создании решений SharePoint Framework можно использовать CSS для определения внешнего вида и функционала вашей настройки. Эта статья описывает, как лучше всего использовать возможности SharePoint Framework и легко создавать стили CSS.</span><span class="sxs-lookup"><span data-stu-id="66e05-p101">When building SharePoint Framework solutions, you can use CSS to define how your customization should look like and behave. This article describes how you can make the best use of the capabilities provided with the SharePoint Framework and build your CSS styles in a robust way.</span></span>

## <a name="sharepoint-framework-customizations-are-part-of-the-page"></a><span data-ttu-id="66e05-105">Настройка SharePoint Framework является частью страницы</span><span class="sxs-lookup"><span data-stu-id="66e05-105">SharePoint Framework customizations are part of the page</span></span>

<span data-ttu-id="66e05-p102">При создании настроек SharePoint с использованием модели надстройки решение изолируется от других элементов на странице. Вне зависимости от того, выполняется ли код в iframe в качестве надстройки либо как иммерсивное приложение, контролирующее всю страницу, на него не влияют другие элементы и стили, определенные на странице.</span><span class="sxs-lookup"><span data-stu-id="66e05-p102">When building SharePoint customizations using the add-in model, the solution is isolated from other elements on the page. Your code is executed either in an iframe, as an add-in part, or as an immersive application taking control of the whole page. In both cases, your code is not affected by other elements and styles defined on the page.</span></span>

<span data-ttu-id="66e05-p103">Решения SharePoint Framework являются частью страницы и полностью интегрируются с моделью DOM этой страницы. И хотя это устраняет ряд ограничений, сопровождающих модель надстройки, ваше решение подвергается риску. Если эта часть страницы не будет явно изолирована, к ней будут применяться все стили CSS, присутствующие на странице, что потенциально может привести к нежелательным результатам. Чтобы избежать таких рисков, нужно определить свои стили CSS таким образом, чтобы они не влияли ни на что другое на странице, кроме вашей настройки.</span><span class="sxs-lookup"><span data-stu-id="66e05-p103">SharePoint Framework solutions are a part of the page and integrate fully with the page's DOM. While this removes a number of restrictions that come with the add-in model, it exposes your solution to a risk. Because it's a part of the page, unless explicitly isolated, all CSS styles present on the page will apply to it, potentially resulting in an experience different from intended. To avoid such risks, you should define your CSS styles in such a way so that they won't affect anything else on the page other than your customization.</span></span>

## <a name="organize-css-files-in-your-solution"></a><span data-ttu-id="66e05-113">Организация файлов CSS в вашем решении</span><span class="sxs-lookup"><span data-stu-id="66e05-113">Organize CSS files in your solution</span></span>

<span data-ttu-id="66e05-p104">Пользовательский интерфейс решений часто состоит из нескольких стандартных блоков. Во многих библиотеках JavaScript эти стандартные блоки называются компонентами. Компонент может быть простым и определять только представление, либо он может быть более сложным и включать состояние и другие компоненты. Разделение решения на несколько компонентов позволяет упростить процесс разработки и облегчает их тестирование и повторное использование в решении.</span><span class="sxs-lookup"><span data-stu-id="66e05-p104">The UI of your solutions often consists of multiple building blocks. In many JavaScript libraries these building blocks are called components. A component can be simple and define only the presentation or it can be more complex and include state and other components. Splitting your solution into multiple components allows you to simplify the development process and makes them easier to test and reuse in your solution.</span></span>

<span data-ttu-id="66e05-p105">Поскольку компоненты определяют представление, часто возникает потребность в стилях CSS. В идеале компоненты должны быть изолированы, чтобы их можно было использовать отдельно. Поэтому следует хранить стили CSS для конкретного компонента и все другие файлы активов вместе с компонентом. Ниже приведен пример структуры приложения React с несколькими компонентами вместе с их файлами CSS.</span><span class="sxs-lookup"><span data-stu-id="66e05-p105">Because components have presentation, they often require CSS styles. Ideally, components should be isolated and be able to be used on their own. With that in mind, it makes perfect sense for you to store CSS styles for the particular component along with all other asset files next to the component. Following, is a sample structure of a React application with a number of components each with its own CSS file.</span></span>

```text
todoWebPart\components
                      \todoList
                               \todoList.tsx
                               \todoList.module.scss
                      \todoItem
                               \todoItem.tsx
                               \todoItem.module.scss
```

## <a name="use-sass"></a><span data-ttu-id="66e05-122">Использование SASS</span><span class="sxs-lookup"><span data-stu-id="66e05-122">Use Sass</span></span>

<span data-ttu-id="66e05-p106">В SharePoint Framework можно использовать и CSS, и SASS. SASS — это надмножество CSS, предлагающее ряд функций, таких как использование переменных, вставки селекторов или использование примесей — все это упрощает работу со стилями CSS и управление ими в долгосрочной перспективе. Полный набор функций см. на веб-сайте [SASS](http://sass-lang.com). Весь действующий CSS также является действительным SASS, что очень полезно, если вы еще не работали с SASS раньше и хотите постепенно изучить его возможности.</span><span class="sxs-lookup"><span data-stu-id="66e05-p106">In the SharePoint Framework you can use both CSS and Sass. Sass is a superset of CSS and offers you a number of features such as using variables, nesting selectors or using mixins - all of which simplify working with and managing CSS styles over long term. For a complete set of features see the [Sass website](http://sass-lang.com). All valid CSS is also valid Sass which is very helpful if you haven't worked with Sass before and want to gradually learn its capabilities.</span></span>

## <a name="avoid-using-ids-in-markup"></a><span data-ttu-id="66e05-127">Избегайте использования ИД в исправлениях</span><span class="sxs-lookup"><span data-stu-id="66e05-127">Avoid using ID's in markup</span></span>

<span data-ttu-id="66e05-p107">Используя SharePoint Framework, вы создаете настройки, которые конечные пользователи добавляют в SharePoint. Невозможно предугадать, сколько раз конкретная настройка будет использоваться на странице. Чтобы избежать проблем, важно всегда предполагать, что на одной странице есть несколько экземпляров вашей настройки. Имея это в виду, следует избегать использования любых ИД в исправлениях. ИД на странице должны быть уникальными, и если пользователь дважды добавит веб-часть на страницу, тем самым он нарушит эту предпосылку, что может привести к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="66e05-p107">Using the SharePoint Framework you build customizations that end-users add to SharePoint. It's impossible to tell upfront if the particular customization will be used only once on a page or if there will be multiple instances of it. To avoid issues, you should always assume that there are multiple instances of your customization on the same page. With that in mind, you should avoid using any ID's in your markup. ID's are meant to be unique on a page and if a user added your web part to the page twice, it would violate this premise possibly leading to errors.</span></span>

<span data-ttu-id="66e05-133">**Не рекомендуем:**</span><span class="sxs-lookup"><span data-stu-id="66e05-133">**Bad practice:**</span></span>

```ts
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

<span data-ttu-id="66e05-134">**Рекомендуем:**</span><span class="sxs-lookup"><span data-stu-id="66e05-134">**Good practice:**</span></span>

```ts
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

## <a name="use-css-modules-to-avoid-styling-conflicts"></a><span data-ttu-id="66e05-135">Использование CSS-модулей для избежания конфликтов стилей</span><span class="sxs-lookup"><span data-stu-id="66e05-135">Use CSS modules to avoid styling conflicts</span></span>

<span data-ttu-id="66e05-p108">Решения SharePoint Framework являются частью страницы. Чтобы стили CSS для одного компонента не влияли на другие элементы на странице, нужно определить селекторы CSS таким образом, чтобы они применялись только к модели DOM вашего решения. Делать это вручную утомительно и потенциально подвержено ошибкам, но SharePoint Framework может сделать это для вас автоматически.</span><span class="sxs-lookup"><span data-stu-id="66e05-p108">SharePoint Framework solutions are a part of the page. To ensure that CSS styles for one component don't affect other elements on the page, you should define your CSS selectors in such a way that they apply only to the DOM of your solution. It's tedious and error-prone to do this manually, but SharePoint Framework can do this automatically for you.</span></span>

<span data-ttu-id="66e05-p109">Чтобы избежать конфликтов стилей, SharePoint Framework использует [модули CSS](https://github.com/css-modules/css-modules). При создании проекта цепочка инструментов SharePoint Framework обрабатывает все файлы с расширением **.module.scss**. Для каждого файла SharePoint Framework считывает все селекторы классов и добавляет к ним уникальное хэш-значение. После этого он записывает обновленные селекторы в промежуточные файлы CSS, которые включены в сгенерированный пакет веб-частей.</span><span class="sxs-lookup"><span data-stu-id="66e05-p109">To help you avoid stylings conflicts, SharePoint Framework uses [CSS modules](https://github.com/css-modules/css-modules). When building the project, the SharePoint Framework toolchain processes all files with the **.module.scss** extension. For each file, it reads all class selectors and appends a unique hash value to them. Once finished, it writes the updated selectors to intermediate CSS files that are included in the generated web part bundle.</span></span>

<span data-ttu-id="66e05-143">Следуя приведенному выше примеру, предположим, что имеются следующие два файла SASS:</span><span class="sxs-lookup"><span data-stu-id="66e05-143">Following the example above, assume you had the following two Sass files:</span></span>

<span data-ttu-id="66e05-144">**todoList.module.scss:**</span><span class="sxs-lookup"><span data-stu-id="66e05-144">**todoList.module.scss:**</span></span>

```scss
.todoList {
  margin: 1em 0;

  .text {
    font-weight: bold;
    font-size: 1.5em;
  }
}
```

<span data-ttu-id="66e05-145">**todoItem.module.scss:**</span><span class="sxs-lookup"><span data-stu-id="66e05-145">**todoItem.module.scss:**</span></span>

```scss
.todoItem {
  padding: 0.5em 1em;

  .text {
    font-size: 0.9em;
  }
}
```

<span data-ttu-id="66e05-146">После создания проекта в папке **lib** появится два созданных файла CSS, представленных ниже (разрывы строк и отступы добавлены для лучшей читаемости):</span><span class="sxs-lookup"><span data-stu-id="66e05-146">After building the project, in the **lib** folder you would see the following two CSS files generated (line breaks and indenting added for readability):</span></span>

<span data-ttu-id="66e05-147">**todoList.module.css:**</span><span class="sxs-lookup"><span data-stu-id="66e05-147">**todoList.module.css:**</span></span>

```css
.todoList_3e9d35f0 {
  margin:1em 0
}

.todoList_3e9d35f0 .text_3e9d35f0 {
  font-weight:700;
  font-size:1.5em
}
```

<span data-ttu-id="66e05-148">**todoItem.module.css:**</span><span class="sxs-lookup"><span data-stu-id="66e05-148">**todoItem.module.css:**</span></span>

```css
.todoItem_f7081cc4 {
  padding:.5em 1em
}

.todoItem_f7081cc4 .text_f7081cc4 {
  font-size:.9em
}
```

<span data-ttu-id="66e05-149">Несмотря на то что в обоих файлах SASS был определен класс **.text**, в созданных файлах CSS к нему добавлены к нему два разных хэша, что делает его уникальным именем класса, характерным для каждого компонента.</span><span class="sxs-lookup"><span data-stu-id="66e05-149">Even though there was a **.text** class defined in both Sass files, notice how in the generated CSS files it has two different hashes appended to it, becoming a unique class name specific to each component.</span></span>

<span data-ttu-id="66e05-p110">Имена классов CSS в модулях CSS генерируются динамически, что делает невозможным непосредственное обращение к ним в коде. Вместо этого при обработке модулей CSS цепочка инструментов SharePoint Framework генерирует файл JavaScript со ссылками на сгенерированные имена классов.</span><span class="sxs-lookup"><span data-stu-id="66e05-p110">The CSS class names in CSS modules are generated dynamically, which makes it impossible for you to refer to them in your code directly. Instead, when processing CSS modules, the SharePoint Framework toolchain generates a JavaScript file with references to the generated class names.</span></span>

<span data-ttu-id="66e05-152">**todoList.module.scss.js:**</span><span class="sxs-lookup"><span data-stu-id="66e05-152">**todoList.module.scss.js:**</span></span>

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

<span data-ttu-id="66e05-153">Чтобы использовать сгенерированные имена классов в вашем коде, сначала импортируйте стили своего компонента, а затем используйте свойство, указывающее на конкретный класс.</span><span class="sxs-lookup"><span data-stu-id="66e05-153">To use the generated class names in your code, you first import the styles of your component and then use the property pointing to the particular class:</span></span>

```ts
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

<span data-ttu-id="66e05-154">Для правильной работы модулей CSS вам необходимо выполнить следующие условия:</span><span class="sxs-lookup"><span data-stu-id="66e05-154">For the CSS modules to work correctly you have to meet the following conditions:</span></span>

* <span data-ttu-id="66e05-p111">Файлы SASS должны иметь расширение **.module.scss**. При использовании расширения **.scss** без **.module** в процессе сборки вы увидите предупреждение. Файл SASS будет передан в промежуточный файл CSS, но имена классов **не будут уникальными**. Этот сценарий можно выбрать, если необходимо переопределить сторонние стили CSS.</span><span class="sxs-lookup"><span data-stu-id="66e05-p111">your Sass files must have the **.module.scss** extension. If you use the **.scss** extension without **.module**, you will see a warning in the build process. The Sass file will be transpiled to an intermediate CSS file but the class names **will not be made unique**. In cases, when you need to override 3rd party CSS styles, this might be intended</span></span>
* <span data-ttu-id="66e05-159">Имена классов CSS должны быть действительными именами переменных JavaScript. Например, они не могут содержать дефисы: `todoList` — правильно, а `todo-list` — неправильно.</span><span class="sxs-lookup"><span data-stu-id="66e05-159">your CSS class names must be valid JavaScript variable names, so for example they cannot contain hyphens: `todoList` is correct but `todo-list` isn't</span></span>
* <span data-ttu-id="66e05-160">Рекомендуем указывать наименования camelCase для классов, но это не обязательно.</span><span class="sxs-lookup"><span data-stu-id="66e05-160">camelCase naming for classes is recommended, but it's not enforced</span></span>

## <a name="wrap-your-css-styles-in-a-class-named-after-the-component"></a><span data-ttu-id="66e05-161">Перенос стилей CSS в класс, названный именем компонента</span><span class="sxs-lookup"><span data-stu-id="66e05-161">Wrap your CSS styles in a class named after the component</span></span>

<span data-ttu-id="66e05-162">Объединив модули CSS с поддержкой SASS наборов правил вложения, можно упростить стили CSS и убедиться, что они не повлияют на другие элементы на странице.</span><span class="sxs-lookup"><span data-stu-id="66e05-162">By combining CSS modules with Sass' support for nesting rule sets you can simplify your CSS styles and ensure that they won't affect other elements on the page.</span></span>

<span data-ttu-id="66e05-p112">При создании стилей CSS для компонента перенесите их в класс с именем компонента. Затем назначьте этот класс корневому элементу компонента.</span><span class="sxs-lookup"><span data-stu-id="66e05-p112">When building CSS styles for a component, wrap them in a class named after the component. Then, in the component, assign that class to the component's root element.</span></span>

<span data-ttu-id="66e05-165">**todoList.module.scss:**</span><span class="sxs-lookup"><span data-stu-id="66e05-165">**todoList.module.scss:**</span></span>

```scss
.todoList {
  a {
    display: block;
  }
}
```

<span data-ttu-id="66e05-166">**TodoList.tsx:**</span><span class="sxs-lookup"><span data-stu-id="66e05-166">**TodoList.tsx:**</span></span>

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

<span data-ttu-id="66e05-167">Ниже представлен примерный вид созданного файла CSS после транспиляции:</span><span class="sxs-lookup"><span data-stu-id="66e05-167">After transpilation, the generated CSS file will look similar to:</span></span>

```css
.todoList_3e9d35f0 a {
  display: block;
}
```

<span data-ttu-id="66e05-168">Поскольку селектор начинается с уникального имени класса, специфичного для компонента, альтернативная презентация будет применяться только к гиперссылкам внутри компонента.</span><span class="sxs-lookup"><span data-stu-id="66e05-168">Because the selector begins with the unique class name, specific to your component, the alternative presentation will apply only to hyperlinks inside your component.</span></span>

## <a name="integrate-office-ui-fabric"></a><span data-ttu-id="66e05-169">Интеграция с Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="66e05-169">Integrate Office UI Fabric</span></span>

<span data-ttu-id="66e05-170">Если ваши настройки будут выглядеть и действовать как стандартные функции SharePoint и Office 365, конечным пользователям будет удобнее с ними работать.</span><span class="sxs-lookup"><span data-stu-id="66e05-170">By making your customizations look and behave like the standard functionality of SharePoint and Office 365 you will make it easier for the end-users to work with them.</span></span> <span data-ttu-id="66e05-171">В Office UI Fabric вы найдете набор элементов управления и стилей, при использовании которых ваши настройки будут идеально вписываться в существующий интерфейс.</span><span class="sxs-lookup"><span data-stu-id="66e05-171">Office UI Fabric offers you a set of controls and styles for use in your customizations to seamlessly integrate with the existing user experience.</span></span> <span data-ttu-id="66e05-172">Дополнительные сведения об использовании Office UI Fabric в SharePoint Framework см. в [руководстве по интеграции Office UI Fabric](office-ui-fabric-integration.md).</span><span class="sxs-lookup"><span data-stu-id="66e05-172">For more information about using Office UI Fabric in the SharePoint Framework, read the [Office UI Fabric integration guide](office-ui-fabric-integration.md).</span></span>

## <a name="use-theme-colors"></a><span data-ttu-id="66e05-173">Использование цветов темы</span><span class="sxs-lookup"><span data-stu-id="66e05-173">Use theme colors</span></span>

<span data-ttu-id="66e05-p114">SharePoint дает пользователям возможность выбирать цвет темы для своих сайтов. В настройках SharePoint Framework нужно следовать теме, выбранной пользователями, чтобы настройка выглядела как неотъемлемая часть сайта и излишне не выделялась. Поскольку тема задана пользователями на их сайте, невозможно предугадать, какие цвета вам следует использовать в настройках, но SharePoint Framework может быстро загружать для вас текущую активную цветовую схему автоматически. Для получения дополнительной информации об этой возможности см. [руководство по использованию цветов темы](./use-theme-colors-in-your-customizations.md).</span><span class="sxs-lookup"><span data-stu-id="66e05-p114">SharePoint allows users to choose the theme color for their sites. In your SharePoint Framework customizations you should follow the theme selected by the users to make your customization look like an integral part of the site rather than unnecessarily stand out. Because the theme is set by users in their site, you cannot tell upfront which colors your customization should use, but SharePoint Framework can dynamically load the currently active color scheme automatically for you. For more information about this capability read the [guide on using theme colors](./use-theme-colors-in-your-customizations.md).</span></span>
