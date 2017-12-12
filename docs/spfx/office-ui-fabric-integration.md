---
title: "Использование Office UI Fabric Core и Fabric React в SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: e1e9ac646257d8875de4097b65b19e680e1f9f25
ms.sourcegitcommit: 3276e9b281b227fb2f1a131ab4ac54ae212ce5cf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2017
---
# <a name="using-office-ui-fabric-core-and-fabric-react-in-sharepoint-framework"></a><span data-ttu-id="9d52c-102">Использование Office UI Fabric Core и Fabric React в SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="9d52c-102">Using Office UI Fabric Core and Fabric React in SPFx client-side web parts</span></span>

<span data-ttu-id="9d52c-p101">Office UI Fabric — это официальная клиентская платформа для создания интерфейсов в Office 365 и SharePoint. SharePoint обеспечивает полную интеграцию с Fabric, благодаря которой корпорация Майкрософт может предоставлять надежный и согласованный язык дизайна в различных решениях на основе SharePoint, таких как современные сайты групп, страницы и списки. Кроме того, платформа Office UI Fabric доступна разработчикам в SharePoint Framework при создании пользовательских решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d52c-p101">The Office UI Fabric is the official front-end framework for building experiences in Office 365 and SharePoint. SharePoint provides seamless integration with Fabric that enables Microsoft to deliver a robust and consistent design language across various SharePoint experiences such as modern team sites, modern pages, and modern lists. Additionally, the Office UI Fabric is available for developers in the SharePoint Framework when building custom SharePoint solutions.</span></span>

## <a name="summary"></a><span data-ttu-id="9d52c-106">Сводка</span><span class="sxs-lookup"><span data-stu-id="9d52c-106">Summary</span></span>

<span data-ttu-id="9d52c-107">Корпорация Майкрософт использует Fabric Core и Fabric React в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d52c-107">Microsoft uses Fabric Core and Fabric React in SharePoint.</span></span> <span data-ttu-id="9d52c-108">Она регулярно выпускает обновления для SharePoint Online, при установке которых также могут обновиться ваши версии Fabric Core и Fabric React.</span><span class="sxs-lookup"><span data-stu-id="9d52c-108">Microsoft regularly pushes updates to SharePoint Online which could also update the Fabric Core and Fabric React versions as well.</span></span> <span data-ttu-id="9d52c-109">Возможны конфликты этих обновлений со сторонними клиентскими решениями, созданными с помощью предыдущих версий Fabric Core и Fabric React. В результате этого в таких модификациях могут возникать исключения.</span><span class="sxs-lookup"><span data-stu-id="9d52c-109">These updates could potentially conflict with third party customer solutions built with previous versions of Fabric Core and Fabric React, which could cause exceptions in those customizations.</span></span> <span data-ttu-id="9d52c-110">Основная причина таких сбоев — использование **глобальных стилей CSS** в обеих библиотеках Fabric.</span><span class="sxs-lookup"><span data-stu-id="9d52c-110">The primary reason for these types of breaks is the use of **Global CSS styles** in both Fabric libraries.</span></span> <span data-ttu-id="9d52c-111">Таких конфликтов следует избегать любой ценой.</span><span class="sxs-lookup"><span data-stu-id="9d52c-111">Such conflicts need to be avoided at all costs.</span></span> 

> <span data-ttu-id="9d52c-112">Трудности с глобальными стилями CSS хорошо описаны в следующей презентации на примере React и JSS: [React CSS в JS](https://speakerdeck.com/vjeux/react-css-in-js).</span><span class="sxs-lookup"><span data-stu-id="9d52c-112">The challenge with Global CSS styles is well explained in the following presentation within the context of React and JS: [React CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js).</span></span>

<span data-ttu-id="9d52c-113">Одно из главных препятствий для обеспечения надежности — использование **глобальных стилей CSS**.</span><span class="sxs-lookup"><span data-stu-id="9d52c-113">In order to achieve reliability, one of the main problems we need to solve is that of **Global CSS styles**. Currently, both Fabric Core and fabric.component.css use global styles.</span></span> <span data-ttu-id="9d52c-114">Это гарантирует, что вместо глобальных имен классов в разметке HTML будут использоваться примеси и переменные Fabric Core в файле объявлений SASS.</span><span class="sxs-lookup"><span data-stu-id="9d52c-114">This accounts to not using global class names in the HTML markup and instead using Fabric Core mixins and variables in the SASS declaration file.</span></span> <span data-ttu-id="9d52c-115">При этом объявления SASS для Fabric Core импортируются из файла SASS, после чего переменные и примеси используются надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="9d52c-115">This involves importing the Fabric Core's SASS declarations in your SASS file and then consuming the variables and mixins appropriately.</span></span> 

## <a name="goals"></a><span data-ttu-id="9d52c-116">Цели</span><span class="sxs-lookup"><span data-stu-id="9d52c-116">Goals</span></span>

<span data-ttu-id="9d52c-117">Цель SharePoint Framework — помочь корпорации Майкрософт и ее клиентам создавать функциональные, привлекательные и согласованные решения на основе SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d52c-117">One of the goals of SharePoint Framework is to allow both Microsoft and customers to build rich, beautiful and consistent solutions on top of SharePoint. Based on that, here are our design principles:</span></span> <span data-ttu-id="9d52c-118">Достижению этих целей способствуют основные принципы разработки.</span><span class="sxs-lookup"><span data-stu-id="9d52c-118">In accordance with these goals, below are the key design  principles:</span></span>

* <span data-ttu-id="9d52c-119">Удобство и надежность для пользователей при использовании Fabric Core и Fabric React в решениях.</span><span class="sxs-lookup"><span data-stu-id="9d52c-119">All customers should be able to smoothly and reliably consume Fabric Core and Fabric React in their solutions.</span></span>
* <span data-ttu-id="9d52c-120">Корпорация Майкрософт должна развертывать обновленные решения, использующие обновленные версии Fabric Core и Fabric React, в SharePoint без конфликтов с решениями клиента.</span><span class="sxs-lookup"><span data-stu-id="9d52c-120">Microsoft will roll out updated experiences that consume updated versions of Fabric Core and Fabric React in SharePoint without conflicting with customer's solutions.</span></span>
* <span data-ttu-id="9d52c-121">Пользователи должны иметь возможность настраивать и переопределять стили, оформление и компоненты в соответствии с потребностями решения.</span><span class="sxs-lookup"><span data-stu-id="9d52c-121">Customers can customize and override the styles, designs, and components to tailor to their solution's needs.</span></span>

<span data-ttu-id="9d52c-122">Office UI Fabric состоит из двух частей, доступных разработчикам:</span><span class="sxs-lookup"><span data-stu-id="9d52c-122">There are two parts of the Office UI Fabric that are available to be used by developers:</span></span>

* [<span data-ttu-id="9d52c-123">Office UI Fabric Core</span><span class="sxs-lookup"><span data-stu-id="9d52c-123">Office UI Fabric Core</span></span>](http://dev.office.com/fabric)

  <span data-ttu-id="9d52c-124">Набор, включающий основные стили, оформление, адаптируемую сетку, анимацию, значки и другие стандартные блоки общего языка дизайна.</span><span class="sxs-lookup"><span data-stu-id="9d52c-124">Office UI Fabric Core a.k.a. Fabric Core - this is a set of core styles, typography, a responsive grid, animations, icons, and other fundamental building blocks of the overall design language.</span></span>

* [<span data-ttu-id="9d52c-125">Office UI Fabric React</span><span class="sxs-lookup"><span data-stu-id="9d52c-125">Office UI Fabric React</span></span>](http://dev.office.com/fabric#/components)

  <span data-ttu-id="9d52c-126">Набор компонентов React, основанных на языке дизайна Fabric, для использования в проектах на основе React.</span><span class="sxs-lookup"><span data-stu-id="9d52c-126">A set of React components built on top of the Fabric design language for use in React-based projects.</span></span>

## <a name="spfx-fabric-core-package"></a><span data-ttu-id="9d52c-127">Пакет SPFx Fabric Core</span><span class="sxs-lookup"><span data-stu-id="9d52c-127">SPFx Fabric Core Package</span></span>

<span data-ttu-id="9d52c-128">Пакет npm с SPFx Fabric Core (sp-office-ui-fabric-core) содержит часть поддерживаемых стилей Fabric Core, которые можно с уверенностью использовать в компоненте SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="9d52c-128">The SPFx Fabric Core npm package - sp-office-ui-fabric-core - contains a subset of supported Fabric Core styles that can be safely consumed within a SharePoint Framework component.</span></span> 

<span data-ttu-id="9d52c-129">В пакете поддерживаются следующие основные стили:</span><span class="sxs-lookup"><span data-stu-id="9d52c-129">The following core styles are supported in the package:</span></span>
- <span data-ttu-id="9d52c-130">шрифтовое оформление;</span><span class="sxs-lookup"><span data-stu-id="9d52c-130">Typography</span></span>
- <span data-ttu-id="9d52c-131">макеты;</span><span class="sxs-lookup"><span data-stu-id="9d52c-131">Layouts</span></span>
- <span data-ttu-id="9d52c-132">цвета;</span><span class="sxs-lookup"><span data-stu-id="9d52c-132">Colors</span></span>
- <span data-ttu-id="9d52c-133">темы;</span><span class="sxs-lookup"><span data-stu-id="9d52c-133">Themes</span></span>
- <span data-ttu-id="9d52c-134">локализация.</span><span class="sxs-lookup"><span data-stu-id="9d52c-134">Localization</span></span>

<span data-ttu-id="9d52c-135">В нем пока что не поддерживаются следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="9d52c-135">The following are not yet supported in the package:</span></span>
- <span data-ttu-id="9d52c-136">анимация;</span><span class="sxs-lookup"><span data-stu-id="9d52c-136">Animations</span></span>
- <span data-ttu-id="9d52c-137">значки.</span><span class="sxs-lookup"><span data-stu-id="9d52c-137">Icons</span></span>

<span data-ttu-id="9d52c-138">Начиная с версии 1.3.4 генератора Yeoman для SharePoint Framework стандартные шаблоны проектов (веб-частей и расширений) включают новый пакет sp-office-ui-fabric-core и используют основные стили из пакета, а не глобальные стили CSS.</span><span class="sxs-lookup"><span data-stu-id="9d52c-138">Starting with the SharePoint Framework yeoman generator version 1.3.4, the default project (web parts and extensions) templates will come setup with the new sp-office-ui-fabric-core package and consume core styles from the package instead of using global CSS styles.</span></span> 

### <a name="updating-existing-projects"></a><span data-ttu-id="9d52c-139">Обновление существующих проектов</span><span class="sxs-lookup"><span data-stu-id="9d52c-139">Updating existing projects</span></span>

<span data-ttu-id="9d52c-140">Чтобы использовать пакет SPFx Fabric Core в имеющемся проекте, установите пакет в качестве зависимости для разработки:</span><span class="sxs-lookup"><span data-stu-id="9d52c-140">To use the SPFx Fabric Core package in your existing project, install the package as dev dependency:</span></span>

```
npm install @microsoft/sp-office-ui-fabric-core --save-dev
```

<span data-ttu-id="9d52c-141">После установки можно импортировать объявления SASS для Fabric Core из файла определений SASS, а затем использовать примеси и переменные, как описано в приведенном ниже разделе.</span><span class="sxs-lookup"><span data-stu-id="9d52c-141">Once installed, you can then import the Fabric Core SASS declarations in your SASS defintion file and use the mixins and variables as decribed in the section below.</span></span> 

### <a name="using-fabric-core-styles"></a><span data-ttu-id="9d52c-142">Использование стилей Fabric Core</span><span class="sxs-lookup"><span data-stu-id="9d52c-142">Using Fabric Core styles</span></span>

<span data-ttu-id="9d52c-143">Чтобы использовать стили Fabric Core, для начала необходимо импортировать объявления SPFabricCore из файла SASS.</span><span class="sxs-lookup"><span data-stu-id="9d52c-143">In order to use the Fabric Core styles first you will need to import the SPFabricCore declarations in your SASS file.</span></span>

> <span data-ttu-id="9d52c-144">Примечание. Убедитесь, что установлен пакет npm sp-office-ui-fabric-core.</span><span class="sxs-lookup"><span data-stu-id="9d52c-144">Note: Make sure you have the sp-office-ui-fabric-core npm package installed.</span></span>

```css
@import '~@microsoft/sp-office-ui-fabric-core/dist/sass/SPFabricCore.scss';
```

<span data-ttu-id="9d52c-145">Теперь вы можете использовать основные стили в качестве примесей и переменных.</span><span class="sxs-lookup"><span data-stu-id="9d52c-145">Now, you can use the core styles as mixins and variables.</span></span>

```css
.row {
    @include ms-Grid-row;
    @include ms-fontColor-white;
    background-color: $ms-color-themeDark;
    padding: 20px;
  }
 ``` 

## <a name="using-office-ui-fabric-react"></a><span data-ttu-id="9d52c-146">Использование Office UI Fabric React</span><span class="sxs-lookup"><span data-stu-id="9d52c-146">Office UI Fabric React Components</span></span>

<span data-ttu-id="9d52c-147">Рекомендуем установить последнюю версию пакета Office UI Fabric React и добавить в пакет явную зависимость от этой конкретной версии.</span><span class="sxs-lookup"><span data-stu-id="9d52c-147">It is recommended to install the latest Office UI Fabric React package and place an explicit dependency on that specific version of the package.</span></span> <span data-ttu-id="9d52c-148">В пакет будут включена компоненты, используемые в решении SPFx — веб-части или расширении (в зависимости от того, для каких целей используются компоненты Fabric React).</span><span class="sxs-lookup"><span data-stu-id="9d52c-148">This will include the components used in your SPFx solution in your component bundle, either the web part or extension depending on where you use the Fabric React components.</span></span> 

> <span data-ttu-id="9d52c-149">Обратите внимание, что Fabric React версий 2.x и ниже не поддерживается в SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="9d52c-149">Please note that Fabric React versions 2.x or older are not supported in SharePoint Framework.</span></span>

<span data-ttu-id="9d52c-150">Установив пакет Fabric React, вы можете импортировать из него необходимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="9d52c-150">Once the Fabric React package is installed, you can import the required components from the Fabric React bundle.</span></span>

```Javascript
//import Button component from Fabric React Button bundle
import { Button } from 'office-ui-fabric-react/lib/Button';

//use it in your component
render() {
  ...
  <div>
    <Button>click me</Button>
  </div>
  ...
}
```

<span data-ttu-id="9d52c-151">Пакет Fabric React включает поддерживаемые стили Fabric Core, используемые в компонентах Fabric React.</span><span class="sxs-lookup"><span data-stu-id="9d52c-151">Fabric React package includes the supported Fabric Core styles used in the Fabric React components.</span></span> <span data-ttu-id="9d52c-152">Рекомендуем импортировать стили Fabric Core из пакета Fabric React, а не sp-office-ui-fabric-core, чтобы обеспечить использование подходящих стилей в компоненте.</span><span class="sxs-lookup"><span data-stu-id="9d52c-152">It is recommended to import the Fabric Core styles from the Fabric React package instead of the sp-office-ui-fabric-core package to ensure the right styles are used in your component.</span></span> 

<span data-ttu-id="9d52c-153">Так как пакет sp-office-ui-fabric-core уже установлен в решении генератором Yeoman, рекомендуем удалить этот пакет, если вы решите использовать компоненты Fabric и уменьшить размер пакета компонентов.</span><span class="sxs-lookup"><span data-stu-id="9d52c-153">Since the sp-office-ui-fabric-core package is already installed in your solution by the yeoman generator, it is recommended to uninstall that package if you decide to use Fabric Components and reduce your component bundle size.</span></span>

```
npm uninstall @microsoft/sp-office-ui-fabric-core --save-dev
```

<span data-ttu-id="9d52c-154">Затем вы можете импортировать основные стили из объявлений SASS, доступных в пакете Fabric React.</span><span class="sxs-lookup"><span data-stu-id="9d52c-154">Then you can import the core styles from the SASS declarations available in the Fabric React packge.</span></span>

```css
@import '~office-ui-fabric-react/dist/sass/References.scss';
```

### <a name="understanding-this-approach-and-its-shortcomings"></a><span data-ttu-id="9d52c-155">Общие сведения об этом подходе и его недостатках</span><span class="sxs-lookup"><span data-stu-id="9d52c-155">Understanding this approach and its shortcomings:</span></span>

<span data-ttu-id="9d52c-156">Компоненты Fabric в решении привязаны к установленной у вас версии Fabric React.</span><span class="sxs-lookup"><span data-stu-id="9d52c-156">Fabric Components in your solution are locked to that specific version of Fabric React you installed.</span></span> <span data-ttu-id="9d52c-157">Чтобы получить новые компоненты (если они доступны в более новой версии пакета), необходимо обновить пакет Fabric React.</span><span class="sxs-lookup"><span data-stu-id="9d52c-157">You will need to update the Fabric React package to get any new components if they are available in a newer package version.</span></span> <span data-ttu-id="9d52c-158">Так как компоненты Fabric включены в пакет компонентов, его размер может увеличиться.</span><span class="sxs-lookup"><span data-stu-id="9d52c-158">Since the Fabric Components are included in the component bundle, it may increase the size of your component bundle.</span></span> <span data-ttu-id="9d52c-159">Однако это единственный официально поддерживаемый подход при использовании Office UI Fabric React в решениях SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="9d52c-159">However, this approach is the only approach that is officially supported when Office UI Fabric React is being used in SharePoint Framework solutions.</span></span>


## <a name="additional-details-on-the-css-challenge-with-office-ui-fabric"></a><span data-ttu-id="9d52c-160">Дополнительные сведения о трудностях с CSS в Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="9d52c-160">Additional Details on the CSS Challenge with Office UI Fabric</span></span>
<span data-ttu-id="9d52c-161">Представленные ниже понятия и ссылки раскрывают суть проблем с использованием Office UI Fabric в контексте клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="9d52c-161">The following concepts and references provide insights on the challenge with Office UI Fabric usage in the context of client-side web parts.</span></span> 

<span data-ttu-id="9d52c-p108">**Глобальные стили CSS** и как избегать их использования любой ценой: это серьезная проблема. На данный момент библиотеки Fabric Core и Fabric React содержат глобальные стили. Отсутствие встроенных в браузеры решений для управления областями стилей делает это очень трудной задачей.</span><span class="sxs-lookup"><span data-stu-id="9d52c-p108">**Global CSS styles** and how to avoid them at all cost: this is a big problem. Today, both Fabric Core and Fabric React have global styles. Lack of any native solutions from the browser to manage the style scoping makes this a very difficult problem.</span></span>
  
  - <span data-ttu-id="9d52c-165">[Области CSS](https://developer.mozilla.org/ru-RU/docs/Web/CSS/:scope) находятся на ранней стадии рассмотрения.</span><span class="sxs-lookup"><span data-stu-id="9d52c-165">[Scope CSS](https://developer.mozilla.org/ru-RU/docs/Web/CSS/:scope) is in early stages of discussion.</span></span> 
  - <span data-ttu-id="9d52c-166">Элементы IFrame плохо подходят для изолирования стилей.</span><span class="sxs-lookup"><span data-stu-id="9d52c-166">iframes are not a good option to isolate styles.</span></span>
  - <span data-ttu-id="9d52c-167">[Веб-компоненты](https://developer.mozilla.org/ru-RU/docs/Web/Web_Components) — еще один стандарт, который включает стили с ограниченной областью действия, но пока только обсуждается.</span><span class="sxs-lookup"><span data-stu-id="9d52c-167">[Web Components](https://developer.mozilla.org/ru-RU/docs/Web/Web_Components) is another standard that talks about scoped styles but is still in discussion stages.</span></span>
  - <span data-ttu-id="9d52c-p109">В [этом](https://speakerdeck.com/vjeux/react-css-in-js) обсуждении хорошо раскрыта суть проблемы. В Интернете есть множество другой документации, посвященной решениям проблемы с глобальными пространствами имен.</span><span class="sxs-lookup"><span data-stu-id="9d52c-p109">[This](https://speakerdeck.com/vjeux/react-css-in-js) discussion explains the problem well. There is plenty of other documentation on the web about the solutions to the global namespace menace.</span></span>
 
<span data-ttu-id="9d52c-p110">**[Специфичность CSS](https://developer.mozilla.org/ru-RU/docs/Web/CSS/Specificity)** и как она связана с веб-интерфейсами. Стили с большей специфичностью переопределяют стили с меньшей специфичностью. Но самое важное — понять, как применяются правила специфичности. Общий порядок приоритетов (по убыванию) выглядит так:</span><span class="sxs-lookup"><span data-stu-id="9d52c-p110">**[CSS Specificity](https://developer.mozilla.org/ru-RU/docs/Web/CSS/Specificity)** and how it applies to web UI. Higher specificity styles override the lower specificity styles, but the key thing to understand is how the specificity rules apply. In general, the precedence order from highest to lowest is as follows:</span></span>
  - <span data-ttu-id="9d52c-173">Атрибут стиля (например, `style="background:red;"`)</span><span class="sxs-lookup"><span data-stu-id="9d52c-173">The style attribute (e.g. `style="background:red;"`)</span></span>
  - <span data-ttu-id="9d52c-174">Селекторы идентификаторов (например, `#myDiv { }`)</span><span class="sxs-lookup"><span data-stu-id="9d52c-174">Id selectors (e.g. `#myDiv { }`)</span></span>
  - <span data-ttu-id="9d52c-175">Селекторы классов (например, `.myCssClass{}`), селекторы атрибутов (например, `[type="radio"]`) и псевдоклассы (например, `:hover`)</span><span class="sxs-lookup"><span data-stu-id="9d52c-175">Class selectors (e.g. `.myCssClass{}`), attributre selectors (e.g. `[type="radio"]`), and pseudo-classes (e.g. `:hover`)</span></span>
  - <span data-ttu-id="9d52c-176">Селекторы типов (например, `h1`)</span><span class="sxs-lookup"><span data-stu-id="9d52c-176">Type selectors (e.g. `h1`)</span></span>

<span data-ttu-id="9d52c-p111">***Порядок загрузки***: если к элементу применяются два класса с одинаковой специфичностью, предпочтение отдается классу, загруженному позже. Как показано в представленном ниже коде, кнопка будет красной. Если изменить порядок тегов стиля, она станет зеленой. Это важное понятие. При его неправильном использовании пользовательский интерфейс начинает зависеть от порядка загрузки, то есть становится несогласованным.</span><span class="sxs-lookup"><span data-stu-id="9d52c-p111">***Loading order*** - If two classes are applied on an element and they have the same specificity, the class that is loaded later takes precedence. As shown in the code below, the button will appear red. If the order of the style tags is changed, the button will appear green. This is an important concept, and if not used correctly, the user experience can become load order dependent (i.e. inconsistent).</span></span>

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

## <a name="other-approaches-considered-and-discarded"></a><span data-ttu-id="9d52c-181">Другие подходы, которые были рассмотрены и отклонены</span><span class="sxs-lookup"><span data-stu-id="9d52c-181">Other Approaches Considered and Discarded</span></span>
<span data-ttu-id="9d52c-182">Ниже представлены дополнительные сведения о других подходах, которые были рассмотрены, но отклонены, так как они не соответствовали ключевым целям и не позволяли разработчикам безопасно использовать стили Office UI Fabric.</span><span class="sxs-lookup"><span data-stu-id="9d52c-182">Here are some additional insights on the other approaches which were considered, but discarded, since they did not achieve the key objectives to enable 3rd party developers to safely use the Office UI Fabric styles.</span></span>

<span data-ttu-id="9d52c-183">**Office UI Fabric Core**</span><span class="sxs-lookup"><span data-stu-id="9d52c-183">**Office UI Fabric Core**</span></span>

<span data-ttu-id="9d52c-p112">Разработчику веб-части не требовалось бы выполнять никаких явных действий, чтобы определения областей работали. Мы планировали решить эту проблему с помощью специфичности CSS и селектора потомков. Разработчики Fabric Core собирались выпустить несколько копий CSS-файла Fabric Core, например `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css` и `fabric-6.0.0-scoped.css`.</span><span class="sxs-lookup"><span data-stu-id="9d52c-p112">The web part developer would not be required to do anything explicitly to get the scoping to work. We planned to solve this problem through CSS specificity and descendant selectors. The Fabric Core team would ship multiple copies of Fabric Core css. e.g. `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css`, `fabric-6.0.0-scoped.css`.</span></span>

<span data-ttu-id="9d52c-p113">Все стили в CSS-файлах с ограниченной областью действия были бы включены в селектор потомков, например `"ms-Fabric-core--v6 ms-Icon--List"`. Во время компиляции инструменты получали бы версию Office UI Fabric Core, с помощью которой была создана веб-часть. Это могла быть версия, входящая в состав SPFx. Кроме того, разработчики веб-частей могли бы явно указывать зависимость от определенной версии Office UI Fabric Core в файле **package.json**.</span><span class="sxs-lookup"><span data-stu-id="9d52c-p113">All the styles in the scoped CSS files would be inside a descendant selector e.g. `"ms-Fabric-core--v6 ms-Icon--List"`. At compile time, the tooling would collect the version of the Office UI Fabric Core the web part was built with. This version could be the one that comes with SPFx. Alternatively, web part developers could specify an explicit dependency on a specific version of Office UI Fabric Core in their **package.json** file.</span></span>

<span data-ttu-id="9d52c-p114">Разделителю веб-части была бы назначена эта область действия, т. е. `<div data-sp-webpart class="ms-Fabric-core--v6">`. Платформа загружала бы определенную основную версию CSS-файла с областью действия на уровне Fabric Core. Если веб-часть была создана с помощью CSS-файла Fabric Core версии 6.0.0, платформа скачивала бы файл `fabric-6-scoped.css` во время загрузки веб-части.</span><span class="sxs-lookup"><span data-stu-id="9d52c-p114">The web part div would be assigned this scope i.e. `<div data-sp-webpart class="ms-Fabric-core--v6">`. The framework would load the specific major version of the Fabric core scoped CSS file. If the web part was built with version 6.0.0 of Fabric core CSS, the framework would download `fabric-6-scoped.css` when the web part was loaded.</span></span>

<span data-ttu-id="9d52c-p115">Остальная часть страницы содержала бы стили Office UI Fabric Core с неограниченной областью действия. Таким образом, согласно правилам специфичности CSS внутри разделителя веб-части имели бы приоритет стили CSS с ограниченной областью действия. Веб-часть и ее содержимое были бы адаптированы к определенной версии Office UI Fabric Core, выбранной разработчиком.</span><span class="sxs-lookup"><span data-stu-id="9d52c-p115">The rest of the page would contain unscoped Office UI Fabric Core styles. This way, as per CSS specificity rules, the scoped CSS would take precedence within the web part div. The web part and its contents would align to the specific version of the Office UI Fabric Core the developer had chosen.</span></span>

<span data-ttu-id="9d52c-197">**Переопределение** стилей Fabric Core не поддерживалось.</span><span class="sxs-lookup"><span data-stu-id="9d52c-197">**Overriding** Fabric Core styles would not be supported.</span></span>  

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

<span data-ttu-id="9d52c-198">После тщательного анализа этой стратегии было принято решение, что у подхода с использованием селектора потомков есть два серьезных недостатка, не позволяющих создать отказоустойчивую веб-часть.</span><span class="sxs-lookup"><span data-stu-id="9d52c-198">After analyzing this strategy for a while it was decided that the descendant selector approach has two serious shortcomings that would make it impossible to build a web part that would never break.</span></span>

<span data-ttu-id="9d52c-p116">**Отсутствие надежной поддержки вложения**. Этот подход работает, только если страница и веб-части Майкрософт используют версию Office UI Fabric Core (т. е. `ms-Icon--List`) с неограниченной областью действия, а сторонние веб-части — только CSS Office UI Fabric Core с ограниченной областью действия, как описано выше. Причина заключается в том, что стиль CSS с ограниченной областью действия, примененный к веб-части, переопределяет CSS с неограниченной областью действия на странице. Обратите внимание: как описывалось ранее, если специфичность двух классов CSS совпадает, то предпочтение отдается классу, загруженному позже. Следовательно, для обеспечения согласованности интерфейса важно, чтобы специфичность класса CSS с ограниченной областью действия была выше.</span><span class="sxs-lookup"><span data-stu-id="9d52c-p116">**Lack of reliable nesting support** - This approach only works if the Microsoft user experience (i.e. page and first party web parts) use an unscoped version of the Office UI Fabric Core. i.e. `ms-Icon--List` while the third party web parts only use scoped Office UI Fabric Core css as explained above. The reason being that the specificity of the scoped CSS applied on the web part overrides unscoped CSS on the page. Keep in mind, as explained above, if CSS specificity of two classes is the same, then their loading order plays a role in how the CSS classes will be applied. The class that loads later will take precedence. Hence, the higher specificity of the scoped CSS is important in getting a consistent experience.</span></span>

<span data-ttu-id="9d52c-p117">Более того, несколько расширений, вложенных друг в друга, не могут использовать разные версии Fabric Core. Например, в приведенном ниже примере применяется только `ms-Fabric-core--v6`.</span><span class="sxs-lookup"><span data-stu-id="9d52c-p117">Further, multiple extensions, one contained in the other, cannot use different Fabric Core versions. For instance, in the following example, only `ms-Fabric-core--v6` would get applied:</span></span>

```HTML
<div className={css('ms-Fabric-core--v6')}>
  { // Rest of the web part UI }
    { // inside of this SPExtension trying to use different Fabric core version does not work }
    <div className={css('ms-Fabric-core--v8')}>
    </div>
</div>
```

<span data-ttu-id="9d52c-207">Ниже представлен более простой пример, иллюстрирующий эту проблему.</span><span class="sxs-lookup"><span data-stu-id="9d52c-207">Here's a more simplistic sample demonstrating the challenge:</span></span>

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

<span data-ttu-id="9d52c-p118">**Утечки из неограниченных классов** — еще одна проблема с селекторами потомков. Обратите внимание, что в приведенном выше примере стили высоты и ширины из неограниченного класса myButton применяются ко всем кнопкам. Это означает, что изменение этого стиля может случайно сделать неработоспособным код HTML, в котором используется разметка с ограниченной областью действия. Допустим, по какой-то причине на уровне приложения мы меняем высоту в классе myButton на 0 пикселей. В результате во всех сторонних веб-частях, использующих класс myButton, будет задана высота в 0 пикселей, что отрицательно скажется на пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="9d52c-p118">**Leakage from unscoped classes** - There is another problem with descendant selectors. Note in the above example, the height and the width styles from the unscoped myButton class are applied to all the buttons. This implies that a change in that style could inadvertently break html using scoped markup. Say for example, for some reason at the app level we decide to make height 0px on the myButton class. That will result in all 3rd party web parts using the myButton class to have a height of 0px (i.e. a serious regression in the user experience).</span></span>


