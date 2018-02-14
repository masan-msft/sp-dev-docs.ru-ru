---
title: "Использование Office UI Fabric Core и Fabric React в SharePoint Framework"
description: "Сведения о пакетах Fabric Core и Fabric React, а также трудности при использовании CSS."
ms.date: 01/24/2018
ms.prod: sharepoint
ms.openlocfilehash: 9d984b1655c07d7732edd442f48dd9e253ad2b82
ms.sourcegitcommit: 53fa577acbc93bfff82c7e521b741df51e9585fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2018
---
# <a name="using-office-ui-fabric-core-and-fabric-react-in-sharepoint-framework"></a><span data-ttu-id="86c4a-103">Использование Office UI Fabric Core и Fabric React в SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="86c4a-103">Using Office UI Fabric Core and Fabric React in SharePoint Framework</span></span>

<span data-ttu-id="86c4a-p101">Office UI Fabric — это официальная клиентская платформа для создания интерфейсов в Office 365 и SharePoint. SharePoint обеспечивает полную интеграцию с Fabric, благодаря которой корпорация Майкрософт может предоставлять надежный и согласованный язык дизайна в различных решениях на основе SharePoint, таких как современные сайты групп, страницы и списки. Кроме того, платформа Office UI Fabric доступна разработчикам в SharePoint Framework при создании пользовательских решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="86c4a-p101">The Office UI Fabric is the official front-end framework for building experiences in Office 365 and SharePoint. SharePoint provides seamless integration with Fabric that enables Microsoft to deliver a robust and consistent design language across various SharePoint experiences such as modern team sites, modern pages, and modern lists. Additionally, the Office UI Fabric is available for developers in the SharePoint Framework when building custom SharePoint solutions.</span></span>

<span data-ttu-id="86c4a-107">Корпорация Майкрософт использует Fabric Core и Fabric React в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="86c4a-107">Microsoft uses Fabric Core and Fabric React in SharePoint.</span></span> <span data-ttu-id="86c4a-108">Она регулярно выпускает обновления для SharePoint Online, при установке которых также могут обновиться ваши версии Fabric Core и Fabric React.</span><span class="sxs-lookup"><span data-stu-id="86c4a-108">Microsoft regularly pushes updates to SharePoint Online which could also update the Fabric Core and Fabric React versions as well.</span></span> <span data-ttu-id="86c4a-109">Возможны конфликты этих обновлений со сторонними клиентскими решениями, созданными с помощью предыдущих версий Fabric Core и Fabric React. В результате этого в таких модификациях могут возникать исключения.</span><span class="sxs-lookup"><span data-stu-id="86c4a-109">These updates could potentially conflict with third party customer solutions built with previous versions of Fabric Core and Fabric React, which could cause exceptions in those customizations.</span></span> <span data-ttu-id="86c4a-110">Основная причина таких сбоев — использование **глобальных стилей CSS** в обеих библиотеках Fabric.</span><span class="sxs-lookup"><span data-stu-id="86c4a-110">The primary reason for these types of breaks is the use of **Global CSS styles** in both Fabric libraries.</span></span> <span data-ttu-id="86c4a-111">Таких конфликтов следует избегать любой ценой.</span><span class="sxs-lookup"><span data-stu-id="86c4a-111">Such conflicts need to be avoided at all costs.</span></span> 

<span data-ttu-id="86c4a-112">Трудности с глобальными стилями CSS хорошо описаны в следующей презентации на примере React и JavaScript: [React CSS в JS](https://speakerdeck.com/vjeux/react-css-in-js).</span><span class="sxs-lookup"><span data-stu-id="86c4a-112">The challenge with Global CSS styles is well explained in the following presentation within the context of React and JS: [React CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js).</span></span>

<span data-ttu-id="86c4a-113">Одно из главных препятствий для обеспечения надежности — использование **глобальных стилей CSS**.</span><span class="sxs-lookup"><span data-stu-id="86c4a-113">In order to achieve reliability, one of the main problems we need to solve is that of **Global CSS styles**.</span></span> <span data-ttu-id="86c4a-114">Это гарантирует, что вместо глобальных имен классов в разметке HTML будут использоваться примеси и переменные Fabric Core в файле объявлений SASS.</span><span class="sxs-lookup"><span data-stu-id="86c4a-114">This accounts to not using global class names in the HTML markup and instead using Fabric Core mixins and variables in the SASS declaration file.</span></span> <span data-ttu-id="86c4a-115">При этом объявления SASS для Fabric Core импортируются из файла SASS, после чего переменные и примеси используются надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="86c4a-115">This involves importing the Fabric Core's SASS declarations in your SASS file and then consuming the variables and mixins appropriately.</span></span> 

## <a name="goals"></a><span data-ttu-id="86c4a-116">Цели</span><span class="sxs-lookup"><span data-stu-id="86c4a-116">Goals</span></span>

<span data-ttu-id="86c4a-117">Цель SharePoint Framework — помочь корпорации Майкрософт и ее клиентам создавать функциональные, привлекательные и согласованные решения на основе SharePoint.</span><span class="sxs-lookup"><span data-stu-id="86c4a-117">The goal of the SharePoint Framework is to allow both Microsoft and customers build rich, beautiful, and consistent user experiences on top of SharePoint.</span></span> 

<span data-ttu-id="86c4a-118">Достижению этих целей способствуют основные принципы разработки, перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="86c4a-118">In accordance with these goals, below are the key design  principles:</span></span>

* <span data-ttu-id="86c4a-119">Удобство и надежность для пользователей при использовании Fabric Core и Fabric React в решениях.</span><span class="sxs-lookup"><span data-stu-id="86c4a-119">Customers should be able to smoothly and reliably consume Fabric Core and Fabric React in their solutions.</span></span>
* <span data-ttu-id="86c4a-120">Корпорация Майкрософт должна развертывать обновленные решения, использующие обновленные версии Fabric Core и Fabric React, в SharePoint без конфликтов с решениями клиента.</span><span class="sxs-lookup"><span data-stu-id="86c4a-120">Microsoft will roll out updated experiences that consume updated versions of Fabric Core and Fabric React in SharePoint without conflicting with customer's solutions.</span></span>
* <span data-ttu-id="86c4a-121">Пользователи должны иметь возможность настраивать и переопределять стили, оформление и компоненты в соответствии с потребностями решения.</span><span class="sxs-lookup"><span data-stu-id="86c4a-121">Customers can customize and override the default styles, designs, and components to tailor the solution's needs.</span></span>

<span data-ttu-id="86c4a-122">Office UI Fabric состоит из двух частей, доступных разработчикам:</span><span class="sxs-lookup"><span data-stu-id="86c4a-122">There are two parts of the Office UI Fabric that are available to be used by developers:</span></span>

* <span data-ttu-id="86c4a-123">[Office UI Fabric Core](https://developer.microsoft.com/ru-RU/fabric).</span><span class="sxs-lookup"><span data-stu-id="86c4a-123">[Office UI Fabric Core](https://developer.microsoft.com/ru-RU/fabric)</span></span> <span data-ttu-id="86c4a-124">Набор, включающий основные стили, оформление, адаптируемую сетку, анимацию, значки и другие стандартные блоки общего языка дизайна.</span><span class="sxs-lookup"><span data-stu-id="86c4a-124">A set of core styles, typography, a responsive grid, animations, icons, and other fundamental building blocks of the overall design language.</span></span>

* <span data-ttu-id="86c4a-125">[Office UI Fabric React](https://developer.microsoft.com/ru-RU/fabric#/components).</span><span class="sxs-lookup"><span data-stu-id="86c4a-125">[Office UI Fabric React](https://developer.microsoft.com/ru-RU/fabric#/components)</span></span> <span data-ttu-id="86c4a-126">Набор компонентов React, основанных на языке дизайна Fabric, для использования в проектах на основе React.</span><span class="sxs-lookup"><span data-stu-id="86c4a-126">A set of React components built on top of the Fabric design language for use in React-based projects.</span></span>

## <a name="office-ui-fabric-core-package"></a><span data-ttu-id="86c4a-127">Пакет Office UI Fabric Core</span><span class="sxs-lookup"><span data-stu-id="86c4a-127">Office UI Fabric Core</span></span>

<span data-ttu-id="86c4a-128">Пакет npm с SharePoint Framework Fabric Core (sp-office-ui-fabric-core) содержит подмножество поддерживаемых стилей Fabric Core, которые можно безопасно использовать в компоненте SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="86c4a-128">The SPFx Fabric Core npm package - sp-office-ui-fabric-core - contains a subset of supported Fabric Core styles that can be safely consumed within a SharePoint Framework component.</span></span> 

<span data-ttu-id="86c4a-129">В пакете поддерживаются следующие основные стили:</span><span class="sxs-lookup"><span data-stu-id="86c4a-129">The following core styles are supported in the package:</span></span>
- <span data-ttu-id="86c4a-130">шрифтовое оформление;</span><span class="sxs-lookup"><span data-stu-id="86c4a-130">Typography</span></span>
- <span data-ttu-id="86c4a-131">макеты;</span><span class="sxs-lookup"><span data-stu-id="86c4a-131">Layouts</span></span>
- <span data-ttu-id="86c4a-132">цвета;</span><span class="sxs-lookup"><span data-stu-id="86c4a-132">Colors</span></span>
- <span data-ttu-id="86c4a-133">темы;</span><span class="sxs-lookup"><span data-stu-id="86c4a-133">Themes</span></span>
- <span data-ttu-id="86c4a-134">локализация.</span><span class="sxs-lookup"><span data-stu-id="86c4a-134">Localization</span></span>

<span data-ttu-id="86c4a-135">В нем пока что не поддерживаются следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="86c4a-135">The following are not yet supported in the package:</span></span>
- <span data-ttu-id="86c4a-136">анимация;</span><span class="sxs-lookup"><span data-stu-id="86c4a-136">Animations</span></span>
- <span data-ttu-id="86c4a-137">значки.</span><span class="sxs-lookup"><span data-stu-id="86c4a-137">Icons</span></span>

<span data-ttu-id="86c4a-138">Начиная с версии 1.3.4 генератора Yeoman для SharePoint Framework стандартные шаблоны проектов (веб-частей и расширений) включают новый пакет sp-office-ui-fabric-core и используют основные стили из пакета, а не глобальные стили CSS.</span><span class="sxs-lookup"><span data-stu-id="86c4a-138">Starting with the SharePoint Framework yeoman generator version 1.3.4, the default project (web parts and extensions) templates will come setup with the new sp-office-ui-fabric-core package and consume core styles from the package instead of using global CSS styles.</span></span> 

### <a name="update-existing-projects"></a><span data-ttu-id="86c4a-139">Обновление существующих проектов</span><span class="sxs-lookup"><span data-stu-id="86c4a-139">Update existing projects</span></span>

<span data-ttu-id="86c4a-140">Чтобы использовать пакет Fabric Core в имеющемся проекте, установите пакет в качестве зависимости для разработки:</span><span class="sxs-lookup"><span data-stu-id="86c4a-140">To use the SPFx Fabric Core package in your existing project, install the package as dev dependency:</span></span>

```
npm install @microsoft/sp-office-ui-fabric-core --save-dev
```

<span data-ttu-id="86c4a-141">После установки можно импортировать объявления SASS для Fabric Core из файла определений SASS, а затем использовать примеси и переменные, как описано в разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="86c4a-141">Once installed, you can then import the Fabric Core SASS declarations in your SASS defintion file and use the mixins and variables as decribed in the section below.</span></span> 

### <a name="use-fabric-core-styles"></a><span data-ttu-id="86c4a-142">Использование стилей Fabric Core</span><span class="sxs-lookup"><span data-stu-id="86c4a-142">Using Fabric Core styles</span></span>

<span data-ttu-id="86c4a-143">Чтобы использовать стили Fabric Core, необходимо импортировать объявления SPFabricCore в файл SASS.</span><span class="sxs-lookup"><span data-stu-id="86c4a-143">In order to use the Fabric Core styles first you will need to import the SPFabricCore declarations in your SASS file.</span></span>

> [!NOTE] 
> <span data-ttu-id="86c4a-144">Убедитесь, что установлен пакет npm sp-office-ui-fabric-core.</span><span class="sxs-lookup"><span data-stu-id="86c4a-144">Note: Make sure you have the sp-office-ui-fabric-core npm package installed.</span></span>

```css
@import '~@microsoft/sp-office-ui-fabric-core/dist/sass/SPFabricCore.scss';
```

<br/>

<span data-ttu-id="86c4a-145">Теперь вы можете использовать основные стили в качестве примесей и переменных.</span><span class="sxs-lookup"><span data-stu-id="86c4a-145">Now, you can use the core styles as mixins and variables.</span></span>

```css
.row {
    @include ms-Grid-row;
    @include ms-fontColor-white;
    background-color: $ms-color-themeDark;
    padding: 20px;
  }
 ``` 

## <a name="office-ui-fabric-react"></a><span data-ttu-id="86c4a-146">Office UI Fabric React</span><span class="sxs-lookup"><span data-stu-id="86c4a-146">Office UI Fabric React</span></span>

<span data-ttu-id="86c4a-147">Рекомендуем установить последнюю версию пакета Office UI Fabric React и добавить в пакет явную зависимость от этой конкретной версии.</span><span class="sxs-lookup"><span data-stu-id="86c4a-147">It is recommended to install the latest Office UI Fabric React package and place an explicit dependency on that specific version of the package.</span></span> <span data-ttu-id="86c4a-148">В пакет будут включены компоненты, используемые в решении SharePoint Framework — веб-части или расширении (в зависимости от того, для каких целей используются компоненты Fabric React).</span><span class="sxs-lookup"><span data-stu-id="86c4a-148">This will include the components used in your SPFx solution in your component bundle, either the web part or extension depending on where you use the Fabric React components.</span></span> 

> [!NOTE] 
> <span data-ttu-id="86c4a-149">Fabric React версий 2.x и ниже не поддерживается в SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="86c4a-149">Please note that Fabric React versions 2.x or older are not supported in SharePoint Framework.</span></span>

<span data-ttu-id="86c4a-150">Установив пакет Fabric React, вы можете импортировать из него необходимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="86c4a-150">Once the Fabric React package is installed, you can import the required components from the Fabric React bundle.</span></span>

```js
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

<span data-ttu-id="86c4a-151">Пакет Fabric React включает поддерживаемые стили Fabric Core, используемые в компонентах Fabric React.</span><span class="sxs-lookup"><span data-stu-id="86c4a-151">Fabric React package includes the supported Fabric Core styles used in the Fabric React components.</span></span> <span data-ttu-id="86c4a-152">Рекомендуем импортировать стили Fabric Core из пакета Fabric React, а не sp-office-ui-fabric-core, чтобы обеспечить использование подходящих стилей в компоненте.</span><span class="sxs-lookup"><span data-stu-id="86c4a-152">It is recommended to import the Fabric Core styles from the Fabric React package instead of the sp-office-ui-fabric-core package to ensure the right styles are used in your component.</span></span> 

<span data-ttu-id="86c4a-153">Так как пакет sp-office-ui-fabric-core уже установлен в решении генератором Yeoman, рекомендуем удалить этот пакет, если вы решите использовать компоненты Fabric и уменьшить размер пакета компонентов.</span><span class="sxs-lookup"><span data-stu-id="86c4a-153">Since the sp-office-ui-fabric-core package is already installed in your solution by the yeoman generator, it is recommended to uninstall that package if you decide to use Fabric Components and reduce your component bundle size.</span></span>

```
npm uninstall @microsoft/sp-office-ui-fabric-core --save-dev
```

<span data-ttu-id="86c4a-154">После этого вы можете импортировать основные стили из объявлений SASS, доступных в пакете Fabric React.</span><span class="sxs-lookup"><span data-stu-id="86c4a-154">Then you can import the core styles from the SASS declarations available in the Fabric React package .</span></span>

```css
@import '~office-ui-fabric-react/dist/sass/References.scss';
```

### <a name="understanding-this-approach-and-its-shortcomings"></a><span data-ttu-id="86c4a-155">Общие сведения об этом подходе и его недостатках</span><span class="sxs-lookup"><span data-stu-id="86c4a-155">Understanding this approach and its shortcomings</span></span>

<span data-ttu-id="86c4a-156">Компоненты Fabric в решении привязаны к установленной у вас версии Fabric React.</span><span class="sxs-lookup"><span data-stu-id="86c4a-156">Fabric Components in your solution are locked to that specific version of Fabric React you installed.</span></span> <span data-ttu-id="86c4a-157">Чтобы получить новые компоненты (если они доступны в более новой версии пакета), необходимо обновить пакет Fabric React.</span><span class="sxs-lookup"><span data-stu-id="86c4a-157">You will need to update the Fabric React package to get any new components if they are available in a newer package version.</span></span> <span data-ttu-id="86c4a-158">Так как компоненты Fabric включены в пакет компонентов, его размер может увеличиться.</span><span class="sxs-lookup"><span data-stu-id="86c4a-158">Since the Fabric Components are included in the component bundle, it may increase the size of your component bundle.</span></span> <span data-ttu-id="86c4a-159">Однако это единственный официально поддерживаемый подход при использовании Office UI Fabric React в решениях SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="86c4a-159">However, this approach is the only approach that is officially supported when Office UI Fabric React is being used in SharePoint Framework solutions.</span></span>


## <a name="the-css-challenge-with-office-ui-fabric"></a><span data-ttu-id="86c4a-160">Трудности с CSS в Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="86c4a-160">Additional details on the CSS challenge with Office UI Fabric</span></span>

<span data-ttu-id="86c4a-161">Представленные ниже понятия и ссылки раскрывают суть проблем с использованием Office UI Fabric в контексте клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="86c4a-161">The following concepts and references provide insights on the challenge with Office UI Fabric usage in the context of client-side web parts.</span></span> 

### <a name="global-css-styles"></a><span data-ttu-id="86c4a-162">Глобальные стилей CSS</span><span class="sxs-lookup"><span data-stu-id="86c4a-162">Global CSS styles</span></span>

<span data-ttu-id="86c4a-163">Как избегать использования глобальных стилей CSS любой ценой — это серьезная проблема.</span><span class="sxs-lookup"><span data-stu-id="86c4a-163">How to avoid Global CSS styles at all costs is a big problem.</span></span> <span data-ttu-id="86c4a-164">На данный момент библиотеки Fabric Core и Fabric React содержат глобальные стили.</span><span class="sxs-lookup"><span data-stu-id="86c4a-164">Today, both Fabric Core and Fabric React have global styles.</span></span> <span data-ttu-id="86c4a-165">Отсутствие встроенных в браузеры решений для управления областями стилей делает это очень трудной задачей.</span><span class="sxs-lookup"><span data-stu-id="86c4a-165">A lack of any native solutions from the browser to manage the style scoping makes this a very difficult problem.</span></span>
  
  - <span data-ttu-id="86c4a-166">[Области CSS](https://developer.mozilla.org/ru-RU/docs/Web/CSS/:scope) находятся на ранней стадии рассмотрения.</span><span class="sxs-lookup"><span data-stu-id="86c4a-166">[Scope CSS](https://developer.mozilla.org/ru-RU/docs/Web/CSS/:scope) is in early stages of discussion.</span></span>
  - <span data-ttu-id="86c4a-167">Элементы IFrame плохо подходят для изолирования стилей.</span><span class="sxs-lookup"><span data-stu-id="86c4a-167">iframes are not a good option to isolate styles.</span></span>
  - <span data-ttu-id="86c4a-168">[Веб-компоненты](https://developer.mozilla.org/ru-RU/docs/Web/Web_Components) — еще один стандарт, который включает стили с ограниченной областью действия, но пока только обсуждается.</span><span class="sxs-lookup"><span data-stu-id="86c4a-168">[Web Components](https://developer.mozilla.org/ru-RU/docs/Web/Web_Components) is another standard that talks about scoped styles but is still in discussion stages.</span></span>
  - <span data-ttu-id="86c4a-169">Суть проблемы хорошо раскрыта в обсуждении [React CSS в JS](https://speakerdeck.com/vjeux/react-css-in-js).</span><span class="sxs-lookup"><span data-stu-id="86c4a-169">[The React: CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js) discussion explains the problem well.</span></span> 
  
<span data-ttu-id="86c4a-170">В Интернете есть множество другой документации, посвященной решениям проблемы с глобальными пространствами имен.</span><span class="sxs-lookup"><span data-stu-id="86c4a-170">This discussion explains the problem well. There is plenty of other documentation on the web about the solutions to the global namespace menace.</span></span>

### <a name="css-specificity"></a><span data-ttu-id="86c4a-171">Специфичность CSS</span><span class="sxs-lookup"><span data-stu-id="86c4a-171">CSS specificity</span></span>

<span data-ttu-id="86c4a-172">Как [правила CSS](https://developer.mozilla.org/ru-RU/docs/Web/CSS/Specificity) применяются к веб-интерфейсу?</span><span class="sxs-lookup"><span data-stu-id="86c4a-172">How [CSS specificity](https://developer.mozilla.org/ru-RU/docs/Web/CSS/Specificity) applies to web UI.</span></span> <span data-ttu-id="86c4a-173">Стили с большей специфичностью переопределяют стили с меньшей специфичностью. Но самое важное — понять, как применяются правила специфичности.</span><span class="sxs-lookup"><span data-stu-id="86c4a-173">CSS Specificity and how it applies to web UI. Higher specificity styles override the lower specificity styles, but the key thing to understand is how the specificity rules apply. In general, the precedence order from highest to lowest is as follows:</span></span> <span data-ttu-id="86c4a-174">Общий порядок приоритетов (по убыванию) выглядит так:</span><span class="sxs-lookup"><span data-stu-id="86c4a-174">In general, the precedence order from highest to lowest is as follows:</span></span>
  - <span data-ttu-id="86c4a-175">атрибут стиля (например, `style="background:red;"`);</span><span class="sxs-lookup"><span data-stu-id="86c4a-175">The style attribute (for example, `style="background:red;"`)</span></span>
  - <span data-ttu-id="86c4a-176">селекторы идентификаторов (`#myDiv { }`);</span><span class="sxs-lookup"><span data-stu-id="86c4a-176">ID selectors (`#myDiv { }`)</span></span>
  - <span data-ttu-id="86c4a-177">селекторы классов (`.myCssClass{}`), селекторы атрибутов (`[type="radio"]`) и псевдоклассы (`:hover`);</span><span class="sxs-lookup"><span data-stu-id="86c4a-177">Class selectors (`.myCssClass{}`), attribute selectors (`[type="radio"]`), and pseudo-classes (`:hover`)</span></span>
  - <span data-ttu-id="86c4a-178">селекторы типов (`h1`).</span><span class="sxs-lookup"><span data-stu-id="86c4a-178">Type selectors (`h1`)</span></span>

<span data-ttu-id="86c4a-179">**Порядок загрузки**.</span><span class="sxs-lookup"><span data-stu-id="86c4a-179">**Loading order**.</span></span> <span data-ttu-id="86c4a-180">Если к элементу применяются два класса с одинаковой специфичностью, предпочтение отдается классу, загруженному позже.</span><span class="sxs-lookup"><span data-stu-id="86c4a-180">If two classes are applied on an element and have the same specificity, the class that is loaded later takes precedence.</span></span> <span data-ttu-id="86c4a-181">Как показано в представленном ниже коде, кнопка будет красной.</span><span class="sxs-lookup"><span data-stu-id="86c4a-181">As shown in the following code, the button appears red.</span></span> <span data-ttu-id="86c4a-182">Если изменить порядок тегов стиля, она станет зеленой.</span><span class="sxs-lookup"><span data-stu-id="86c4a-182">If the order of the style tags is changed, the button appears green.</span></span> <span data-ttu-id="86c4a-183">Это важное понятие. При его неправильном использовании пользовательский интерфейс начинает зависеть от порядка загрузки, то есть становится несогласованным.</span><span class="sxs-lookup"><span data-stu-id="86c4a-183">This is an important concept, and if not used correctly, the user experience can become load order-dependent (that is, inconsistent).</span></span>

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

## <a name="other-approaches-considered-and-discarded"></a><span data-ttu-id="86c4a-184">Другие подходы, которые были рассмотрены и отклонены</span><span class="sxs-lookup"><span data-stu-id="86c4a-184">Other approaches considered and discarded</span></span>

<span data-ttu-id="86c4a-185">Ниже представлены дополнительные сведения о других подходах, которые были рассмотрены, но отклонены, так как не соответствовали ключевым целям и не позволяли сторонним разработчикам безопасно использовать стили Office UI Fabric.</span><span class="sxs-lookup"><span data-stu-id="86c4a-185">Here are some additional insights on the other approaches which were considered, but discarded, since they did not achieve the key objectives to enable 3rd party developers to safely use the Office UI Fabric styles.</span></span>

### <a name="office-ui-fabric-core"></a><span data-ttu-id="86c4a-186">Office UI Fabric Core</span><span class="sxs-lookup"><span data-stu-id="86c4a-186">Office UI Fabric Core</span></span>

<span data-ttu-id="86c4a-187">Разработчику веб-части не требовалось бы выполнять никаких явных действий, чтобы определения областей работали.</span><span class="sxs-lookup"><span data-stu-id="86c4a-187">The web part developer would not be required to do anything explicitly to get the scoping to work.</span></span> <span data-ttu-id="86c4a-188">Мы планировали решить эту проблему с помощью специфичности CSS и селектора потомков.</span><span class="sxs-lookup"><span data-stu-id="86c4a-188">We planned to solve this problem through CSS specificity and descendant selectors.</span></span> <span data-ttu-id="86c4a-189">Разработчики Fabric Core собирались выпустить несколько копий CSS-файла Fabric Core (например, `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css` и `fabric-6.0.0-scoped.css`).</span><span class="sxs-lookup"><span data-stu-id="86c4a-189">The Fabric Core team would ship multiple copies of Fabric Core css (for example, `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css`, `fabric-6.0.0-scoped.css`).</span></span>

<span data-ttu-id="86c4a-190">Все стили в CSS-файлах с ограниченной областью действия были бы включены в селектор потомков, например `"ms-Fabric-core--v6 ms-Icon--List"`.</span><span class="sxs-lookup"><span data-stu-id="86c4a-190">All the styles in the scoped CSS files would be inside a descendant selector, for example `"ms-Fabric-core--v6 ms-Icon--List"`.</span></span> <span data-ttu-id="86c4a-191">Во время компиляции инструменты получали бы версию Office UI Fabric Core, с помощью которой была создана веб-часть.</span><span class="sxs-lookup"><span data-stu-id="86c4a-191">At compile time, the tooling would collect the version of the Office UI Fabric Core that the web part was built with.</span></span> <span data-ttu-id="86c4a-192">Это могла быть версия, входящая в состав SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="86c4a-192">This version could be the one that comes with SharePoint Framework.</span></span> <span data-ttu-id="86c4a-193">Кроме того, разработчики веб-частей могли бы явно указывать зависимость от определенной версии Office UI Fabric Core в файле **package.json**.</span><span class="sxs-lookup"><span data-stu-id="86c4a-193">Alternatively, web part developers could specify an explicit dependency on a specific version of Office UI Fabric Core in their **package.json** file.</span></span>

<span data-ttu-id="86c4a-194">Разделителю веб-части была бы назначена эта область действия, т. е. `<div data-sp-webpart class="ms-Fabric-core--v6">`.</span><span class="sxs-lookup"><span data-stu-id="86c4a-194">The web part div would be assigned this scope, that is `<div data-sp-webpart class="ms-Fabric-core--v6">`.</span></span> <span data-ttu-id="86c4a-195">Платформа загружала бы определенную основную версию CSS-файла с областью действия на уровне Fabric Core.</span><span class="sxs-lookup"><span data-stu-id="86c4a-195">The Framework would load the specific major version of the Fabric Core-scoped CSS file.</span></span> <span data-ttu-id="86c4a-196">Если веб-часть была создана с помощью CSS-файла Fabric Core версии 6.0.0, платформа скачивала бы файл `fabric-6-scoped.css` во время загрузки веб-части.</span><span class="sxs-lookup"><span data-stu-id="86c4a-196">If the web part was built with version 6.0.0 of the Fabric Core CSS, the Framework would download `fabric-6-scoped.css` when the web part was loaded.</span></span>

<span data-ttu-id="86c4a-197">Остальная часть страницы содержала бы стили Office UI Fabric Core с неограниченной областью действия.</span><span class="sxs-lookup"><span data-stu-id="86c4a-197">The rest of the page would contain unscoped Office UI Fabric Core styles.</span></span> <span data-ttu-id="86c4a-198">Таким образом, согласно правилам специфичности CSS внутри разделителя веб-части имели бы приоритет стили CSS с ограниченной областью действия.</span><span class="sxs-lookup"><span data-stu-id="86c4a-198">This way, as per CSS specificity rules, the scoped CSS would take precedence within the web part div.</span></span> <span data-ttu-id="86c4a-199">Веб-часть и ее содержимое приспосабливались бы к определенной версии Office UI Fabric Core, выбранной разработчиком.</span><span class="sxs-lookup"><span data-stu-id="86c4a-199">The web part and its contents would align to the specific version of the Office UI Fabric Core that the developer had chosen.</span></span>

<span data-ttu-id="86c4a-200">*Переопределение* стилей Fabric Core не поддерживалось бы.</span><span class="sxs-lookup"><span data-stu-id="86c4a-200">*Overriding* Fabric Core styles would not be supported.</span></span>  

```js
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

### <a name="shortcomings-of-this-strategy"></a><span data-ttu-id="86c4a-201">Недостатки этой стратегии</span><span class="sxs-lookup"><span data-stu-id="86c4a-201">Shortcomings of this strategy</span></span>

<span data-ttu-id="86c4a-202">После тщательного анализа этой стратегии было принято решение, что у подхода с использованием селектора потомков есть два серьезных недостатка, не позволяющих создать отказоустойчивую веб-часть.</span><span class="sxs-lookup"><span data-stu-id="86c4a-202">After analyzing this strategy for a while it was decided that the descendant selector approach has two serious shortcomings that would make it impossible to build a web part that would never break.</span></span>

#### <a name="lack-of-reliable-nesting-support"></a><span data-ttu-id="86c4a-203">Отсутствие надежной поддержки вложения</span><span class="sxs-lookup"><span data-stu-id="86c4a-203">Lack of reliable nesting support</span></span>

<span data-ttu-id="86c4a-204">Этот подход работает, только если страница и веб-части Майкрософт используют версию Office UI Fabric Core (т. е. `ms-Icon--List`) с неограниченной областью действия, а сторонние веб-части — только CSS Office UI Fabric Core с ограниченной областью действия, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="86c4a-204">This approach only works if the Microsoft user experience (that is, page and first-party web parts) use an unscoped version of the Office UI Fabric Core such as `ms-Icon--List`, while the third-party web parts only use scoped Office UI Fabric Core CSS as explained earlier.</span></span> 

<span data-ttu-id="86c4a-205">Это обусловлено тем, что CSS с ограниченной областью действия, примененный к веб-части, переопределяет CSS с неограниченной областью действия на странице.</span><span class="sxs-lookup"><span data-stu-id="86c4a-205">The reason being that the specificity of the scoped CSS applied on the web part overrides the unscoped CSS on the page.</span></span> <span data-ttu-id="86c4a-206">Обратите внимание: как описывалось ранее, если специфичность двух классов CSS совпадает,</span><span class="sxs-lookup"><span data-stu-id="86c4a-206">Keep in mind, as explained earlier, that if CSS specificity of the two classes is the same, their loading order plays a role in how the CSS classes are applied.</span></span> <span data-ttu-id="86c4a-207">то предпочтение отдается классу, загруженному позже.</span><span class="sxs-lookup"><span data-stu-id="86c4a-207">The class that loads later takes precedence.</span></span> <span data-ttu-id="86c4a-208">Следовательно, для обеспечения согласованности интерфейса важно, чтобы специфичность класса CSS с ограниченной областью действия была выше.</span><span class="sxs-lookup"><span data-stu-id="86c4a-208">Hence, the higher specificity of the scoped CSS is important in getting a consistent experience.</span></span>

<span data-ttu-id="86c4a-209">Кроме того, несколько расширений, вложенных друг в друга, не могут использовать разные версии Fabric Core.</span><span class="sxs-lookup"><span data-stu-id="86c4a-209">Further, multiple extensions, one contained in the other, cannot use different Fabric Core versions. For instance, in the following example, only  would get applied:</span></span> <span data-ttu-id="86c4a-210">Например, в примере ниже применяется только `ms-Fabric-core--v6`.</span><span class="sxs-lookup"><span data-stu-id="86c4a-210">In the following example, only `ms-Fabric-core--v6` would get applied:</span></span>

```HTML
<div className={css('ms-Fabric-core--v6')}>
  { // Rest of the web part UI }
    { // inside of this SPExtension trying to use different Fabric core version does not work }
    <div className={css('ms-Fabric-core--v8')}>
    </div>
</div>
```

<br/>

<span data-ttu-id="86c4a-211">Ниже представлен более простой пример, иллюстрирующий эту проблему.</span><span class="sxs-lookup"><span data-stu-id="86c4a-211">Here's a more simplistic sample demonstrating the challenge:</span></span>

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

#### <a name="leakage-from-unscoped-classes"></a><span data-ttu-id="86c4a-212">Утечки из неограниченных классов</span><span class="sxs-lookup"><span data-stu-id="86c4a-212">Leakage from unscoped classes</span></span>

<span data-ttu-id="86c4a-213">Есть еще одна проблема с селекторами потомков.</span><span class="sxs-lookup"><span data-stu-id="86c4a-213">There is another problem with descendant selectors.</span></span> <span data-ttu-id="86c4a-214">Обратите внимание, что в предыдущем примере стили высоты и ширины из неограниченного класса myButton применяются ко всем кнопкам.</span><span class="sxs-lookup"><span data-stu-id="86c4a-214">Note in the previous example that the height and the width styles from the unscoped myButton class are applied to all the buttons.</span></span> <span data-ttu-id="86c4a-215">Это означает, что изменение этого стиля может случайно сделать неработоспособным код HTML, в котором используется разметка с ограниченной областью действия.</span><span class="sxs-lookup"><span data-stu-id="86c4a-215">This implies that a change in that style could inadvertently break HTML by using scoped markup.</span></span> 

<span data-ttu-id="86c4a-216">Допустим, по какой-то причине на уровне приложения мы меняем высоту в классе myButton на 0 пикселей.</span><span class="sxs-lookup"><span data-stu-id="86c4a-216">Say for example, for some reason at the app level we decide to make height 0 px on the myButton class.</span></span> <span data-ttu-id="86c4a-217">Как следствие, во всех сторонних веб-частях, использующих класс myButton, будет задана высота в 0 пикселей, что отрицательно скажется на пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="86c4a-217">That results in all third-party web parts that use the myButton class to have a height of 0 px (that is, a serious regression in the user experience).</span></span>

## <a name="see-also"></a><span data-ttu-id="86c4a-218">См. также</span><span class="sxs-lookup"><span data-stu-id="86c4a-218">See also</span></span>

- [<span data-ttu-id="86c4a-219">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="86c4a-219">Overview of the SharePoint Framework</span></span>](sharepoint-framework-overview.md)




