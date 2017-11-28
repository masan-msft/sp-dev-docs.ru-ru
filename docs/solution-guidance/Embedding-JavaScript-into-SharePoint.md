---
title: "Внедрение JavaScript в SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: efb690bf90fcba627287e6d25f8bb3bb0442752a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="embedding-javascript-into-sharepoint"></a><span data-ttu-id="9fb55-102">Внедрение JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9fb55-102">Embedding JavaScript into SharePoint</span></span>

<span data-ttu-id="9fb55-103">Пространства имен можно использовать во избежание конфликтов между настроек JavaScript и стандартных SharePoint JavaScript или JavaScript пользовательские настройки, развернутые другими разработчиками.</span><span class="sxs-lookup"><span data-stu-id="9fb55-103">You can use namespaces to avoid conflicts between your JavaScript customizations and standard SharePoint JavaScript or JavaScript customizations deployed by other developers.</span></span> 

<span data-ttu-id="9fb55-104">[Примеры/PnP разработчик офисных решений](https://github.com/SharePoint/PnP/) и решений часто включают код JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9fb55-104">The [OfficeDev/PnP](https://github.com/SharePoint/PnP/) samples and solutions often include JavaScript code.</span></span> <span data-ttu-id="9fb55-105">Чтобы упростить понимание методов, в этих примерах обычно просты и пространства имен следует использовать при внедрении код JavaScript в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9fb55-105">In order to make the techniques easy to understand, these samples are usually simple and do not use namespaces when embedding JavaScript code into SharePoint.</span></span> <span data-ttu-id="9fb55-106">Важно убедитесь, что выполнены действия при внедрении PnP примеры в решения, описанные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="9fb55-106">It is important to ensure that you follow the simple steps outlined in this article when you incorporate PnP samples into your solutions.</span></span>

## <a name="why-using-namespaces-is-important"></a><span data-ttu-id="9fb55-107">Почему важна с помощью пространства имен</span><span class="sxs-lookup"><span data-stu-id="9fb55-107">Why using namespaces is important</span></span>
<span data-ttu-id="9fb55-108"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb55-108"></span></span>

<span data-ttu-id="9fb55-109">JavaScript — это слабо типизированный язык.</span><span class="sxs-lookup"><span data-stu-id="9fb55-109">JavaScript is a loosely typed language.</span></span> <span data-ttu-id="9fb55-110">Если определение переменной или функции, а переменной или функции с тем же именем уже существует в текущем контексте, новое значение или реализации заменяет существующий.</span><span class="sxs-lookup"><span data-stu-id="9fb55-110">If you define a variable or function, and a variable or function with the same name already exists in the current context, the new value or implementation will replace the existing one.</span></span>
<span data-ttu-id="9fb55-111">В результате при внедрении код JavaScript в SharePoint, можно легко переопределить стандартный код SharePoint JavaScript или пользовательские настройки, развернутые другими разработчиками.</span><span class="sxs-lookup"><span data-stu-id="9fb55-111">As a result, when you embed JavaScript code into SharePoint, it is easy to override standard SharePoint JavaScript code or customizations deployed by other developers.</span></span>
<span data-ttu-id="9fb55-112">Это может вызвать конфликты, которые может быть трудно определить и исправить.</span><span class="sxs-lookup"><span data-stu-id="9fb55-112">This can create conflicts that might be hard to identify and debug.</span></span>

<span data-ttu-id="9fb55-113">Чтобы избежать этого, мы рекомендуем использовать настраиваемые пространства имен в коде JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9fb55-113">To avoid this, we recommend that you use custom namespaces for your JavaScript code.</span></span>

## <a name="how-to-use-namespaces"></a><span data-ttu-id="9fb55-114">Как использовать пространства имен</span><span class="sxs-lookup"><span data-stu-id="9fb55-114">How to use namespaces</span></span>
<span data-ttu-id="9fb55-115"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb55-115"></span></span>

<span data-ttu-id="9fb55-116">В следующем примере показано простое шаблон для упорядочивания код JavaScript в пространства имен и классы.</span><span class="sxs-lookup"><span data-stu-id="9fb55-116">The following example shows a simple pattern used to organize JavaScript code in namespaces and classes.</span></span>

```JavaScript
var MySolution = MySolution || {};

MySolution.MyClass1 = (function () {
    // private members
    var privateVar1 = 1;
    var privateVar2 = 2;
    
    function privateFunction1(){
      return "";
    }
    
    return {
        // public interface
        myFunction1: function() {
          return privateVar1;
        },
        myFunction2: function(){
          return privateVar2;
        }
    };
})();
```

<span data-ttu-id="9fb55-117">Как можно вызывать функции, определенные в открытый интерфейс:</span><span class="sxs-lookup"><span data-stu-id="9fb55-117">Functions defined in public interface can be invoked as:</span></span>

```JavaScript
MySolution.MyClass1.myFunction1();

MySolution.MyClass1.myFunction2();
```

<span data-ttu-id="9fb55-118">Так как весь код использует пользовательское пространство имен *MySolution* , можно избежать конфликтов имен.</span><span class="sxs-lookup"><span data-stu-id="9fb55-118">Because all your code uses the custom *MySolution* namespace, you can avoid any naming conflicts.</span></span>

## <a name="namespaces-and-minimal-download-strategy-mds"></a><span data-ttu-id="9fb55-119">Пространства имен и стратегия минимальной загрузки (MDS)</span><span class="sxs-lookup"><span data-stu-id="9fb55-119">Namespaces and Minimal Download Strategy (MDS)</span></span>

<span data-ttu-id="9fb55-120">[Стратегия минимальной загрузки компонента](https://msdn.microsoft.com/en-us/library/office/dn456544.aspx) включена глобальные пространства имен и переменные очищаются на MDS навигации.</span><span class="sxs-lookup"><span data-stu-id="9fb55-120">With the [Minimal Download Strategy Feature](https://msdn.microsoft.com/en-us/library/office/dn456544.aspx) enabled, Global Namespaces and Variables are cleared on MDS navigation.</span></span>   
<span data-ttu-id="9fb55-121">Чтобы сохранить пространства имен, объявите ее в качестве:</span><span class="sxs-lookup"><span data-stu-id="9fb55-121">To retain your Namespace, declare it as:</span></span>

```JavaScript
    Type.registerNamespace('MySolution');
```

<span data-ttu-id="9fb55-122">Пространство имен типа относится к SharePoint, для универсального использования библиотеки JavaScript:</span><span class="sxs-lookup"><span data-stu-id="9fb55-122">The Type Namespace is specific to SharePoint,  for a generic JavaScript library use:</span></span>

```JavaScript
if (window.hasOwnProperty('Type')) {
    Type.registerNamespace('MySolution');
} else {
    window.MySolution = window.MySolution || {};
}
```

#### <a name="namespaces-mds-and-csr-client-side-rendering"></a><span data-ttu-id="9fb55-123">Пространства имен, MDS и CSR (отображение со стороны клиента)</span><span class="sxs-lookup"><span data-stu-id="9fb55-123">Namespaces, MDS and CSR (Client Side Rendering)</span></span>

<span data-ttu-id="9fb55-124">``RegisterModuleInit`` Функция объявляет верной ``Type`` пространства имен.</span><span class="sxs-lookup"><span data-stu-id="9fb55-124">The ``RegisterModuleInit`` function declares a proper ``Type`` Namespace.</span></span>  
<span data-ttu-id="9fb55-125">Файлы, присоединенные с помощью JSLink, **не** повторно выполняются на панели навигации MDS, используйте функции AsyncDeltaManager, которые.</span><span class="sxs-lookup"><span data-stu-id="9fb55-125">Files attached with JSLink are **not** re-executed on MDS navigation, use the AsyncDeltaManager functions for that.</span></span>

### <a name="resources"></a><span data-ttu-id="9fb55-126">Ресурсы:</span><span class="sxs-lookup"><span data-stu-id="9fb55-126">Resources:</span></span>

* [<span data-ttu-id="9fb55-127">Виктор Wilén - правильный способ выполнения функций javascript в SharePoint MDS сайтам с поддержкой</span><span class="sxs-lookup"><span data-stu-id="9fb55-127">Wictor Wilén - The correct way to execute javascript functions in SharePoint MDS enabled sites</span></span>](http://www.wictorwilen.se/the-correct-way-to-execute-javascript-functions-in-sharepoint-2013-mds-enabled-sites)
* [<span data-ttu-id="9fb55-128">AsyncDeltaManager Хью дерева - разработка SharePoint JavaScript контексте —</span><span class="sxs-lookup"><span data-stu-id="9fb55-128">Hugh Wood - SharePoint JavaScript context development - AsyncDeltaManager</span></span>](https://www.spcaf.com/blog/sharepoint-javascript-context-development-part-4-the-way-of-the-async-delta-manager/)
* [<span data-ttu-id="9fb55-129">Андерсон Marc - выполнение JavaScript после MDS (нагрузки повторное)</span><span class="sxs-lookup"><span data-stu-id="9fb55-129">Marc Anderson - Execute JavaScript after MDS (re)load</span></span>](http://blog.symprogress.com/2013/09/sharepoint-2013-execute-javascript-function-after-mds-load/)
