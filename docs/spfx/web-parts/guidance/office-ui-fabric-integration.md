# <a name="using-office-ui-fabric-core-and-fabric-react-in-spfx-client-side-web-parts"></a><span data-ttu-id="ffcd6-101">Использование Office UI Fabric Core и Fabric React в клиентских веб-частях SPFx</span><span class="sxs-lookup"><span data-stu-id="ffcd6-101">Using Office UI Fabric Core and Fabric React in SPFx client-side web parts</span></span>

#### <span data-ttu-id="ffcd6-p101">**Важно!** Для использования компонентов Office UI Fabric React необходимо обновить имеющиеся проекты, чтобы они использовали *@microsoft/sp-build-web@1.0.1* или более поздней версии. Дополнительные сведения вы найдете в инструкциях в конце этой статьи.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p101">**Important:** You must upgrade existing projects to use *@microsoft/sp-build-web@1.0.1* or later in order to use the Office UI Fabric React components. See the instructions at the end of this article for additional information.</span></span>

<span data-ttu-id="ffcd6-p102">Office UI Fabric — это официальная клиентская платформа для создания интерфейсов в Office 365 и SharePoint. SharePoint обеспечивает полную интеграцию с Fabric, благодаря которой корпорация Майкрософт может предоставлять надежный и согласованный язык дизайна в различных решениях на основе SharePoint, таких как современные сайты групп, страницы и списки. Кроме того, платформа Office UI Fabric доступна разработчикам в SharePoint Framework при создании пользовательских решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p102">The Office UI Fabric is the official front-end framework for building experiences in Office 365 and SharePoint. SharePoint provides seamless integration with Fabric that enables Microsoft to deliver a robust and consistent design language across various SharePoint experiences such as modern team sites, modern pages, and modern lists. Additionally, the Office UI Fabric is available for developers in the SharePoint Framework when building custom SharePoint solutions.</span></span>

> <span data-ttu-id="ffcd6-p103">Способы интеграции и использования Office UI Fabric по-прежнему находятся в стадии разработки. Этот документ содержит сведения о текущем состоянии платформы для разработчиков SPFx. Вскоре мы опубликуем окончательный план.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p103">Integration and usage of the Office UI Fabric is still a work in progress. The purpose of this document is to provide a status update to SPFx developers. Very soon we will publish a final plan.</span></span>

## <a name="goals"></a><span data-ttu-id="ffcd6-110">Цели</span><span class="sxs-lookup"><span data-stu-id="ffcd6-110">Goals</span></span>

<span data-ttu-id="ffcd6-111">Office UI Fabric состоит из двух частей, доступных разработчикам:</span><span class="sxs-lookup"><span data-stu-id="ffcd6-111">There are two parts of the Office UI Fabric that are available to be used by developers:</span></span>

  1. <span data-ttu-id="ffcd6-p104">[Office UI Fabric Core](http://dev.office.com/fabric), или Fabric Core, — это набор, включающий основные стили, оформление, адаптируемую сетку, анимацию, значки и другие стандартные блоки общего языка дизайна.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p104">[Office UI Fabric Core](http://dev.office.com/fabric) a.k.a. Fabric Core - this is a set of core styles, typography, a responsive grid, animations, icons, and other fundamental building blocks of the overall design language.</span></span>

  2. <span data-ttu-id="ffcd6-p105">[Office UI Fabric React](http://dev.office.com/fabric#/components), или Fabric React, — это пакет, содержащий набор компонентов React, основанных на языке дизайна Fabric.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p105">[Office UI Fabric React](http://dev.office.com/fabric#/components) a.k.a. Fabric React - this package contains a set of React components built on top of the Fabric design language.</span></span>
  
<span data-ttu-id="ffcd6-p106">Одна из целей SharePoint Framework — предоставить корпорации Майкрософт и ее клиентам возможность создавать функциональные, привлекательные и согласованные решения на основе SharePoint. Достижению этой цели способствуют наши принципы разработки:</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p106">Some of the goals of the SharePoint Framework are to allow both Microsoft and customers to build rich, beautiful, and consistent solutions on top of SharePoint. In accordance with these goals, here are our design principles:</span></span>

* <span data-ttu-id="ffcd6-118">Удобство и надежность для всех пользователей при использовании Fabric Core и Fabric React в решениях.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-118">All customers should be able to smoothly and reliably consume Fabric Core and Fabric React in their solutions.</span></span>
* <span data-ttu-id="ffcd6-119">Корпорация Майкрософт должна развертывать обновленные решения, использующие обновленные версии Fabric Core и Fabric React, в SharePoint без конфликтов с решениями клиента.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-119">Microsoft will roll out updated experiences that consume updated versions of Fabric Core and Fabric React in SharePoint without conflicting with customer's solutions.</span></span>
* <span data-ttu-id="ffcd6-120">Пользователи должны иметь возможность настраивать и переопределять стили, оформление и компоненты в соответствии с потребностями решения.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-120">Customers can customize and override the styles, designs, and components to tailor to their solution's needs.</span></span>
* <span data-ttu-id="ffcd6-121">Пользователи должны иметь возможность создавать решения на платформах, не основанных на React.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-121">Customers should be able to build solutions with non-React based frameworks.</span></span>

## <a name="summary"></a><span data-ttu-id="ffcd6-122">Сводка</span><span class="sxs-lookup"><span data-stu-id="ffcd6-122">Summary</span></span>

<span data-ttu-id="ffcd6-p107">Корпорация Майкрософт использует Fabric Core и Fabric React в SharePoint. Корпорация Майкрософт регулярно выпускает обновления для SharePoint Online, а решения для SharePoint, скорее всего, продолжат обновлять используемые ими версии Fabric Core и Fabric React. Возможны конфликты этих обновлений со сторонними решениями, созданными с помощью предыдущих версий Fabric Core и Fabric React. В результате этого в модификациях могут возникать исключения. Основная причина таких сбоев — использование **глобальных стилей CSS** в обеих библиотеках Fabric. Таких конфликтов следует избегать во что бы то ни стало.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p107">Microsoft uses Fabric Core and Fabric React in SharePoint. Microsoft regularly pushes updates to SharePoint Online and SharePoint experiences are likely to continue updating the version of Fabric Core and Fabric React used. These updates could potentially conflict with third party solutions built with previous versions of Fabric Core and Fabric React, which could cause exceptions in those customizations. The primary reason for these types of breaks is the use of **Global CSS styles** in both Fabric libraries. Such conflicts need to be avoided at all costs.</span></span> 

<span data-ttu-id="ffcd6-p108">Одно из главных препятствий для обеспечения надежности — использование **глобальных стилей CSS**. В настоящее время как Fabric Core, так и fabric.component.css используют глобальные стили.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p108">In order to achieve reliability, one of the main problems we need to solve is that of **Global CSS styles**. Currently, both Fabric Core and fabric.component.css use global styles.</span></span>

<span data-ttu-id="ffcd6-p109">По этим причинам пользовательские решения пока не могут безопасно использовать компоненты Office UI Fabric. Однако мы понимаем, что Fabric Core и Fabric React необходимы разработчикам для создания решений. Мы постараемся устранить эту проблему как можно скорее.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p109">For these reasons, currently, customer solutions cannot yet safely use portions of the Office UI Fabric. However, we understand that developers need Fabric Core and Fabric React to build their solutions. We are working to resolve this as quickly as possible.</span></span>

<span data-ttu-id="ffcd6-133">Ниже представлена сводка поддерживаемых в настоящее время вариантов использования Office UI Fabric с решением SharePoint Framework в зависимости от выбранной платформы JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-133">Here's a summary of currently supported options for using the Office UI Fabric within SharePoint Framework solutions based on the JavaScript framework selected:</span></span>

- <span data-ttu-id="ffcd6-134">React: безопасно использовать Office UI Fabric можно только с помощью **статических ссылок** на компоненты Fabric React.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-134">React - You can only use the Office UI Fabric safely by **statically linking** to the Fabric React components</span></span>
- <span data-ttu-id="ffcd6-135">Другие библиотеки JS: использование Office UI Fabric с решениями SharePoint Framework **не** поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-135">Other JS libraries - Usage of the Office UI Fabric within a SharePoint Framework solution is **not** supported</span></span>

> <span data-ttu-id="ffcd6-p110">Пример текущих сложностей с управлением версиями: при создании веб-часть использует класс `ms-Icon--List`. Позже в Fabric меняется определение этого класса. Веб-часть, опирающаяся на предыдущую реализацию, может выйти из строя. Аналогичный случай: допустим, веб-часть использует класс `ms-Button` из Fabric React. Затем разработчики Fabric React кардинально меняют реализацию объекта Button и стилей класса `ms-Button`. Скорее всего, это выведет веб-часть из строя.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p110">An example of the current versioning challenge: A web part consumes the class `ms-Icon--List` when they build their web part. At a later date, Fabric decides to change the definition of this class. The web part that had made an assumption regarding the previous implementation can break. Similarly, let's say, the web part uses the class `ms-Button` from Fabric React. Then the Fabric React team later changes the implementation of the Button in a big way along with the styles in the `ms-Button` class. That would likely break the web part.</span></span>

> <span data-ttu-id="ffcd6-142">Трудности с глобальными стилями CSS хорошо описаны в следующей презентации на примере React и JSS: [React CSS в JS](https://speakerdeck.com/vjeux/react-css-in-js).</span><span class="sxs-lookup"><span data-stu-id="ffcd6-142">The challenge with Global CSS styles is well explained in the following presentation within the context of React and JS: [React CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js).</span></span>

## <a name="how-to-use-the-office-ui-fabric-react-in-a-safe-way-in-your-solution"></a><span data-ttu-id="ffcd6-143">Безопасное использование Office UI Fabric React в решении</span><span class="sxs-lookup"><span data-stu-id="ffcd6-143">How to use the Office UI Fabric React in a Safe Way in Your Solution</span></span>

<span data-ttu-id="ffcd6-144">Ниже представлены рекомендации по безопасному и надежному использованию Fabric в веб-частях на основе React.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-144">Here are the recommendations for using Fabric in React based web parts in a safe and reliable way:</span></span>

- <span data-ttu-id="ffcd6-p111">Разработчикам веб-частей необходимо явно указывать зависимость от библиотеки Fabric React версии 2.0 в файле **package.json**: `"office-ui-fabric-react":"2.34.2"`. Обратите внимание, что Fabric React версий выше 2.x не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p111">Web part developers should place an explicit dependency on the specific version of Fabric React version 2.0 in their **package.json** file `"office-ui-fabric-react":"2.34.2"`. Please note, Fabric React versions older than 2.x are not supported.</span></span>
- <span data-ttu-id="ffcd6-p112">Разработчикам веб-частей необходимо добавлять **статические ссылки** на компоненты Fabric React. При этом компонент Fabric React включается в пакет веб-части. Благодаря этому, если реализация объекта Button на уровне страницы изменится, это не окажет отрицательного влияния на веб-часть.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p112">Web part developers need to **statically link** to the Fabric React components. This includes the Fabric React component in your web part bundle. This will ensure that if the page level implementation of the Button were to change, it will not affect your web part adversely.</span></span>
- <span data-ttu-id="ffcd6-p113">**Переопределять** стили компонентов Fabric React следует осторожно и только в локальной области. Разработчик может переопределять стили с помощью пользовательских классов CSS с тегами `!important` и style. В обоих случаях специфичность этих классов будет выше, чем у классов компонентов. Обратите внимание, что при переопределении с помощью простого класса могут возникнуть проблемы с порядком загрузки. Например, если класс `ms-Button` загружается после вашего класса, предпочтение отдается классу ms-Button, так как у них одинаковая специфичность.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p113">**Overriding** Fabric React component styles should be done only sparingly and within a local scope. A developer can override using custom CSS classes with `!important` and style tags. Both will have higher specificity than the component classes. Please note, if you override using a simple class, then you may run into load order issues. i.e. If `ms-Button` loads after your class, it will take precedence because their specificity is the same.</span></span>
- <span data-ttu-id="ffcd6-p114">**Темы** должны работать без изменений. От разработчика не требуется дополнительных усилий.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p114">**Theming** should just work as is. No extra work is required on the part of the developer.</span></span>

<span data-ttu-id="ffcd6-157">В приведенном ниже фрагменте кода показано, как создавать статические и динамические ссылки на библиотеки.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-157">The following code snippet shows how to perform static and dynamic linking of libraries:</span></span>

```Javascript
  // This sample demonstrates how static linking should be done for Fabric React components.
  // Remember to explicitly add a dependency on a specific version of 
  // office-ui-fabric-react in your package.json file.

  // correct - static linking.
  import { Button } from 'office-ui-fabric-react/lib/Button';

  // incorrect - dynamic linking.
  import { Button } from '@microsoft/office-ui-fabric-react';

  render() {
    ...
    <div>
      <Button>click me</Button>
    </div>
    ...
  }
```

<span data-ttu-id="ffcd6-158">***Общие сведения об этом подходе и его недостатках***</span><span class="sxs-lookup"><span data-stu-id="ffcd6-158">***Understanding this approach and its shortcomings:***</span></span>

- <span data-ttu-id="ffcd6-p115">Компоненты веб-части привязаны к той версии Fabric React, которая использовалась при создании веб-части. Они не будут автоматически обновляться вместе с соответствующей страницей. Чтобы адаптировать веб-часть к новым версиям Fabric React, вам потребуется обновлять ее вручную.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p115">Components in your web part are locked to the version of Fabric React you used when you built the web part. They will not automatically evolve with the surrounding page. You will need to manually update your web part to adapt to newer versions of Fabric React.</span></span>
- <span data-ttu-id="ffcd6-162">Страница может работать медленнее, так как может загружаться больше стилей CSS, но она будет надежной.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-162">The page may be less performant as it may load more CSS, but it will be reliable.</span></span>
- <span data-ttu-id="ffcd6-p116">Статические ссылки увеличивают размер пакета веб-части, но динамические могут не работать в будущих версиях SharePoint Online. Статические ссылки — это единственный официально поддерживаемый подход при использовании Office UI Fabric React в решениях SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p116">Static linking bloats up your web part bundle, but dynamic linking is too fragile considering future updates to be introduced in SharePoint Online. Static linking is the only approach that is officially supported when Office UI Fabric React is being used in SharePoint Framework solutions.</span></span>

### <a name="currently-unsupported-features"></a><span data-ttu-id="ffcd6-165">Неподдерживаемые в настоящее время компоненты</span><span class="sxs-lookup"><span data-stu-id="ffcd6-165">Currently unsupported features</span></span>

- <span data-ttu-id="ffcd6-p117">**Office UI Fabric Core**: в реализации Fabric Core используются текущие глобальные стили, например `.ms-Icon--List`, поэтому не существует надежного способа использовать Fabric Core в веб-части без потенциальных проблем в будущем. Ведутся работы над устранением этой проблемы, а дополнительные сведения будут публиковаться по мере изменения ситуации.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p117">**Office UI Fabric Core**: The Fabric Core implementation currently uses global styles e.g. `.ms-Icon--List` and hence there is no safe way to use Fabric core in your web part without potential challenges in the future. Work is being done to address this challenge and more details will be shared when the situation changes.</span></span>

- <span data-ttu-id="ffcd6-p118">**fabric.components.css**: этот файл содержит глобальные классы, конфликтующие с Fabric React. Например, класс `.ms-Button` из библиотеки fabric.component.css будет переопределять стили кнопок в компоненте Button из Fabric React. Если включить файл fabric.component.css в веб-часть, соответствующая страница или другие веб-части на этой странице могут выйти из строя. Мы работаем над решением и скоро выпустим обновление.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p118">**fabric.components.css**: This file contains global classes that conflict with Fabric React. e.g. `.ms-Button` in fabric.component.css will override the Button styles in a Fabric React Button component. Including fabric.component.css in a web part is bound to break the surrounding page or other web parts on the page. We are working on a solution and will release an update shortly.</span></span>


## <a name="using-the-office-ui-fabric-with-non-react-based-web-parts"></a><span data-ttu-id="ffcd6-172">Использование Office UI Fabric с веб-частями, не основанными на React</span><span class="sxs-lookup"><span data-stu-id="ffcd6-172">Using the Office UI Fabric with Non-React Based Web Parts</span></span>

<span data-ttu-id="ffcd6-p119">Использование Office UI Fabric с веб-частями, не основанными на React, в настоящее время не поддерживается, а с такими реализациями могут возникать непредвиденные проблемы после выпуска новой версии Office UI Fabric. Мы разрабатываем надежный механизм интеграции для **Office UI Fabric Core**, **fabric.component.css** и **веб-частей не на React**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p119">Using the Office UI Fabric with non-React based web parts is currently not supported and implementations could experience unexpected issues when newer versions of the Office UI Fabric are released. We are working on creating a reliable integration story for **Office UI Fabric Core**, **fabric.component.css**, and **Non-React based web parts**.</span></span> 

## <a name="additional-details-on-the-css-challenge-with-office-ui-fabric"></a><span data-ttu-id="ffcd6-175">Дополнительные сведения о трудностях с CSS в Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="ffcd6-175">Additional Details on the CSS Challenge with Office UI Fabric</span></span>
<span data-ttu-id="ffcd6-176">Представленные ниже понятия и ссылки раскрывают суть проблем с использованием Office UI Fabric в контексте клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-176">The following concepts and references provide insights on the challenge with Office UI Fabric usage in the context of client-side web parts.</span></span> 

<span data-ttu-id="ffcd6-p120">**Глобальные стили CSS** и как избегать их использования любой ценой: это серьезная проблема. На данный момент библиотеки Fabric Core и Fabric React содержат глобальные стили. Отсутствие встроенных в браузеры решений для управления областями стилей делает это очень трудной задачей.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p120">**Global CSS styles** and how to avoid them at all cost: this is a big problem. Today, both Fabric Core and Fabric React have global styles. Lack of any native solutions from the browser to manage the style scoping makes this a very difficult problem.</span></span>
  
  - <span data-ttu-id="ffcd6-180">[Области CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/:scope) находятся на ранней стадии рассмотрения.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-180">[Scope CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/:scope) is in early stages of discussion.</span></span> 
  - <span data-ttu-id="ffcd6-181">Элементы IFrame плохо подходят для изолирования стилей.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-181">iframes are not a good option to isolate styles.</span></span>
  - <span data-ttu-id="ffcd6-182">[Веб-компоненты](https://developer.mozilla.org/en-US/docs/Web/Web_Components) — еще один стандарт, который включает стили с ограниченной областью действия, но пока только обсуждается.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-182">[Web Components](https://developer.mozilla.org/en-US/docs/Web/Web_Components) is another standard that talks about scoped styles but is still in discussion stages.</span></span>
          
    <span data-ttu-id="ffcd6-p121">В [этом](https://speakerdeck.com/vjeux/react-css-in-js) обсуждении хорошо раскрыта суть проблемы. В Интернете есть множество другой документации, посвященной решениям проблемы с глобальными пространствами имен.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p121">[This](https://speakerdeck.com/vjeux/react-css-in-js) discussion explains the problem well. There is plenty of other documentation on the web about the solutions to the global namespace menace.</span></span>
 
<span data-ttu-id="ffcd6-p122">**[Специфичность CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)** и как она связана с веб-интерфейсами. Стили с большей специфичностью переопределяют стили с меньшей специфичностью. Но самое важное — понять, как применяются правила специфичности. Общий порядок приоритетов (по убыванию) выглядит так:</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p122">**[CSS Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)** and how it applies to web UI. Higher specificity styles override the lower specificity styles, but the key thing to understand is how the specificity rules apply. In general, the precedence order from highest to lowest is as follows:</span></span>
  - <span data-ttu-id="ffcd6-188">Атрибут стиля (например, `style="background:red;"`)</span><span class="sxs-lookup"><span data-stu-id="ffcd6-188">The style attribute (e.g. `style="background:red;"`)</span></span>
  - <span data-ttu-id="ffcd6-189">Селекторы идентификаторов (например, `#myDiv { }`)</span><span class="sxs-lookup"><span data-stu-id="ffcd6-189">Id selectors (e.g. `#myDiv { }`)</span></span>
  - <span data-ttu-id="ffcd6-190">Селекторы классов (например, `.myCssClass{}`), селекторы атрибутов (например, `[type="radio"]`) и псевдоклассы (например, `:hover`)</span><span class="sxs-lookup"><span data-stu-id="ffcd6-190">Class selectors (e.g. `.myCssClass{}`), attributre selectors (e.g. `[type="radio"]`), and pseudo-classes (e.g. `:hover`)</span></span>
  - <span data-ttu-id="ffcd6-191">Селекторы типов (например, `h1`)</span><span class="sxs-lookup"><span data-stu-id="ffcd6-191">Type selectors (e.g. `h1`)</span></span>

<span data-ttu-id="ffcd6-p123">***Порядок загрузки***: если к элементу применяются два класса с одинаковой специфичностью, предпочтение отдается классу, загруженному позже. Как показано в представленном ниже коде, кнопка будет красной. Если изменить порядок тегов стиля, она станет зеленой. Это важное понятие. При его неправильном использовании пользовательский интерфейс начинает зависеть от порядка загрузки, то есть становится несогласованным.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p123">***Loading order*** - If two classes are applied on an element and they have the same specificity, the class that is loaded later takes precedence. As shown in the code below, the button will appear red. If the order of the style tags is changed, the button will appear green. This is an important concept, and if not used correctly, the user experience can become load order dependent (i.e. inconsistent).</span></span>

```HTML
<style>
  .greenButton { color: green; }
</style>
<style>
  .redButton { color: red; }
</style>
<body>
  <button class="greenButton redButton"></button>
</body>
```

## <a name="other-approaches-considered-and-discarded"></a><span data-ttu-id="ffcd6-196">Другие подходы, которые были рассмотрены и отклонены</span><span class="sxs-lookup"><span data-stu-id="ffcd6-196">Other Approaches Considered and Discarded</span></span>
<span data-ttu-id="ffcd6-197">Ниже представлены дополнительные сведения о других подходах, которые были рассмотрены, но отклонены, так как они не соответствовали ключевым целям и не позволяли разработчикам безопасно использовать стили Office UI Fabric.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-197">Here are some additional insights on the other approaches which were considered, but discarded, since they did not achieve the key objectives to enable 3rd party developers to safely use the Office UI Fabric styles.</span></span>

<span data-ttu-id="ffcd6-198">**Office UI Fabric Core**</span><span class="sxs-lookup"><span data-stu-id="ffcd6-198">**Office UI Fabric Core**</span></span>

<span data-ttu-id="ffcd6-p124">Разработчику веб-части не требовалось бы выполнять никаких явных действий, чтобы определения областей работали. Мы планировали решить эту проблему с помощью специфичности CSS и селектора потомков. Разработчики Fabric Core собирались выпустить несколько копий CSS-файла Fabric Core, например `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css` и `fabric-6.0.0-scoped.css`.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p124">The web part developer would not be required to do anything explicitly to get the scoping to work. We planned to solve this problem through CSS specificity and descendant selectors. The Fabric Core team would ship multiple copies of Fabric Core css. e.g. `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css`, `fabric-6.0.0-scoped.css`.</span></span>

<span data-ttu-id="ffcd6-p125">Все стили в CSS-файлах с ограниченной областью действия были бы включены в селектор потомков, например `"ms-Fabric-core--v6 ms-Icon--List"`. Во время компиляции инструменты получали бы версию Office UI Fabric Core, с помощью которой была создана веб-часть. Это могла быть версия, входящая в состав SPFx. Кроме того, разработчики веб-частей могли бы явно указывать зависимость от определенной версии Office UI Fabric Core в файле **package.json**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p125">All the styles in the scoped CSS files would be inside a descendant selector e.g. `"ms-Fabric-core--v6 ms-Icon--List"`. At compile time, the tooling would collect the version of the Office UI Fabric Core the web part was built with. This version could be the one that comes with SPFx. Alternatively, web part developers could specify an explicit dependency on a specific version of Office UI Fabric Core in their **package.json** file.</span></span>

<span data-ttu-id="ffcd6-p126">Разделителю веб-части была бы назначена эта область действия, т. е. `<div data-sp-webpart class="ms-Fabric-core--v6">`. Платформа загружала бы определенную основную версию CSS-файла с областью действия на уровне Fabric Core. Если веб-часть была создана с помощью CSS-файла Fabric Core версии 6.0.0, платформа скачивала бы файл `fabric-6-scoped.css` во время загрузки веб-части.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p126">The web part div would be assigned this scope i.e. `<div data-sp-webpart class="ms-Fabric-core--v6">`. The framework would load the specific major version of the Fabric core scoped CSS file. If the web part was built with version 6.0.0 of Fabric core CSS, the framework would download `fabric-6-scoped.css` when the web part was loaded.</span></span>

<span data-ttu-id="ffcd6-p127">Остальная часть страницы содержала бы стили Office UI Fabric Core с неограниченной областью действия. Таким образом, согласно правилам специфичности CSS внутри разделителя веб-части имели бы приоритет стили CSS с ограниченной областью действия. Веб-часть и ее содержимое были бы адаптированы к определенной версии Office UI Fabric Core, выбранной разработчиком.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p127">The rest of the page would contain unscoped Office UI Fabric Core styles. This way, as per CSS specificity rules, the scoped CSS would take precedence within the web part div. The web part and its contents would align to the specific version of the Office UI Fabric Core the developer had chosen.</span></span>

<span data-ttu-id="ffcd6-212">**Переопределение** стилей Fabric Core не поддерживалось.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-212">**Overriding** Fabric Core styles would not be supported.</span></span>  

```Javascript
// Sample of how the scoping would work.
import { SPComponentLoader } from '@microsoft/sp-loader';

export default class MyWebPart {
    constructor() {
        super();

        SPComponentLoader.loadCss('https://static2.sharepointonline.com/files/fabric/office-ui-fabric-core/6.0.0/css/fabric-6.0.0.scoped.css');
    }
}

protected render(): void {
  <div className={css('ms-Fabric-core--v6')}>
    { // Rest of the web part UI }
  </div>
}
```

<span data-ttu-id="ffcd6-213">После тщательного анализа этой стратегии было принято решение, что у подхода с использованием селектора потомков есть два серьезных недостатка, не позволяющих создать отказоустойчивую веб-часть.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-213">After analyzing this strategy for a while it was decided that the descendant selector approach has two serious shortcomings that would make it impossible to build a web part that would never break.</span></span>

<span data-ttu-id="ffcd6-p128">**Отсутствие надежной поддержки вложения**. Этот подход работает, только если страница и веб-части Майкрософт используют версию Office UI Fabric Core (т. е. `ms-Icon--List`) с неограниченной областью действия, а сторонние веб-части — только CSS Office UI Fabric Core с ограниченной областью действия, как описано выше. Причина заключается в том, что стиль CSS с ограниченной областью действия, примененный к веб-части, переопределяет CSS с неограниченной областью действия на странице. Обратите внимание: как описывалось ранее, если специфичность двух классов CSS совпадает, то предпочтение отдается классу, загруженному позже. Следовательно, для обеспечения согласованности интерфейса важно, чтобы специфичность класса CSS с ограниченной областью действия была выше.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p128">**Lack of reliable nesting support** - This approach only works if the Microsoft user experience (i.e. page and first party web parts) use an unscoped version of the Office UI Fabric Core. i.e. `ms-Icon--List` while the third party web parts only use scoped Office UI Fabric Core css as explained above. The reason being that the specificity of the scoped CSS applied on the web part overrides unscoped CSS on the page. Keep in mind, as explained above, if CSS specificity of two classes is the same, then their loading order plays a role in how the CSS classes will be applied. The class that loads later will take precedence. Hence, the higher specificity of the scoped CSS is important in getting a consistent experience.</span></span>

<span data-ttu-id="ffcd6-p129">Более того, несколько расширений, вложенных друг в друга, не могут использовать разные версии Fabric Core. Например, в приведенном ниже примере применяется только `ms-Fabric-core--v6`.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p129">Further, multiple extensions, one contained in the other, cannot use different Fabric Core versions. For instance, in the following example, only `ms-Fabric-core--v6` would get applied:</span></span>

```HTML
<div className={css('ms-Fabric-core--v6')}>
  { // Rest of the web part UI }
    { // inside of this SPExtension trying to use different Fabric core version does not work }
    <div className={css('ms-Fabric-core--v8')}>
    </div>
</div>
```

<span data-ttu-id="ffcd6-222">Ниже представлен более простой пример, иллюстрирующий эту проблему.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-222">Here's a more simplistic sample demonstrating the challenge:</span></span>

```HTML
<html>
<head>
  <title>CSS specifity test</title>
  <style>
  .myButton {
      background-color: brown;
      color: brown;
      height: 20px;
      width: 40px;
  }
  </style>
  <style>
  .scope2 .myButton {
      background-color: green;
      color: green;
  }
  </style>
  <style>
  .scope3 .myButton {
      background-color: yellow;
      color: yellow;
  }
  </style>
  <style>
  .scope1 .myButton {
      background-color: red;
      color: red;
  }
  </style>
</head>
<body>
  <div>
    <span>These tests demonstrate descendant selectors, nesting and load order problems.</span>

    <div>
      <br/>
      <span>This test depicts that a descendant selector with the same specificity does not allow nesting.
      All buttons below do not take the innermost scope (i.e. they should be different colors), but they are all red.
      Further, if you change the ordering of the style tags, the colors will change. (i.e. the UI is load order dependant.)</span> 
      <div class='scope1'>
        <button class='myButton'</button>
        <div class='scope2'>
          <button class='myButton'></button>
          <div class='scope3'>
            <button class='myButton'></button>
          </div>
        </div>
      </div>
    </div>
  </div>
</body>
</html>
```

<span data-ttu-id="ffcd6-p130">**Утечки из неограниченных классов** — еще одна проблема с селекторами потомков. Обратите внимание, что в приведенном выше примере стили высоты и ширины из неограниченного класса myButton применяются ко всем кнопкам. Это означает, что изменение этого стиля может случайно сделать неработоспособным код HTML, в котором используется разметка с ограниченной областью действия. Допустим, по какой-то причине на уровне приложения мы меняем высоту в классе myButton на 0 пикселей. В результате во всех сторонних веб-частях, использующих класс myButton, будет задана высота в 0 пикселей, что отрицательно скажется на пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-p130">**Leakage from unscoped classes** - There is another problem with descendant selectors. Note in the above example, the height and the width styles from the unscoped myButton class are applied to all the buttons. This implies that a change in that style could inadvertently break html using scoped markup. Say for example, for some reason at the app level we decide to make height 0px on the myButton class. That will result in all 3rd party web parts using the myButton class to have a height of 0px (i.e. a serious regression in the user experience).</span></span>

## <a name="updating-an-existing-project"></a><span data-ttu-id="ffcd6-228">Обновление существующего проекта</span><span class="sxs-lookup"><span data-stu-id="ffcd6-228">Updating an existing project</span></span>

<span data-ttu-id="ffcd6-229">В файле `package.json` проекта обновите зависимость `@microsoft/sp-build-web` до версии 1.0.1 или выше, удалите каталог `node_modules` проекта и выполните команду `npm install`.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-229">In your project's `package.json`, update the `@microsoft/sp-build-web` dependency to at least version 1.0.1, delete your project's `node_modules` directory, and run `npm install`.</span></span>

