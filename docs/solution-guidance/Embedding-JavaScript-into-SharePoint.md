---
title: "Внедрение JavaScript в SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: efb690bf90fcba627287e6d25f8bb3bb0442752a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="embedding-javascript-into-sharepoint"></a>Внедрение JavaScript в SharePoint

Пространства имен можно использовать во избежание конфликтов между настроек JavaScript и стандартных SharePoint JavaScript или JavaScript пользовательские настройки, развернутые другими разработчиками. 

[Примеры/PnP разработчик офисных решений](https://github.com/SharePoint/PnP/) и решений часто включают код JavaScript. Чтобы упростить понимание методов, в этих примерах обычно просты и пространства имен следует использовать при внедрении код JavaScript в SharePoint. Важно убедитесь, что выполнены действия при внедрении PnP примеры в решения, описанные в этой статье.

## <a name="why-using-namespaces-is-important"></a>Почему важна с помощью пространства имен
<a name="sectionSection0"> </a>

JavaScript — это слабо типизированный язык. Если определение переменной или функции, а переменной или функции с тем же именем уже существует в текущем контексте, новое значение или реализации заменяет существующий.
В результате при внедрении код JavaScript в SharePoint, можно легко переопределить стандартный код SharePoint JavaScript или пользовательские настройки, развернутые другими разработчиками.
Это может вызвать конфликты, которые может быть трудно определить и исправить.

Чтобы избежать этого, мы рекомендуем использовать настраиваемые пространства имен в коде JavaScript.

## <a name="how-to-use-namespaces"></a>Как использовать пространства имен
<a name="sectionSection1"> </a>

В следующем примере показано простое шаблон для упорядочивания код JavaScript в пространства имен и классы.

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

Как можно вызывать функции, определенные в открытый интерфейс:

```JavaScript
MySolution.MyClass1.myFunction1();

MySolution.MyClass1.myFunction2();
```

Так как весь код использует пользовательское пространство имен *MySolution* , можно избежать конфликтов имен.

## <a name="namespaces-and-minimal-download-strategy-mds"></a>Пространства имен и стратегия минимальной загрузки (MDS)

[Стратегия минимальной загрузки компонента](https://msdn.microsoft.com/en-us/library/office/dn456544.aspx) включена глобальные пространства имен и переменные очищаются на MDS навигации.   
Чтобы сохранить пространства имен, объявите ее в качестве:

```JavaScript
    Type.registerNamespace('MySolution');
```

Пространство имен типа относится к SharePoint, для универсального использования библиотеки JavaScript:

```JavaScript
if (window.hasOwnProperty('Type')) {
    Type.registerNamespace('MySolution');
} else {
    window.MySolution = window.MySolution || {};
}
```

#### <a name="namespaces-mds-and-csr-client-side-rendering"></a>Пространства имен, MDS и CSR (отображение со стороны клиента)

``RegisterModuleInit`` Функция объявляет верной ``Type`` пространства имен.  
Файлы, присоединенные с помощью JSLink, **не** повторно выполняются на панели навигации MDS, используйте функции AsyncDeltaManager, которые.

### <a name="resources"></a>Ресурсы:

* [Виктор Wilén - правильный способ выполнения функций javascript в SharePoint MDS сайтам с поддержкой](http://www.wictorwilen.se/the-correct-way-to-execute-javascript-functions-in-sharepoint-2013-mds-enabled-sites)
* [AsyncDeltaManager Хью дерева - разработка SharePoint JavaScript контексте —](https://www.spcaf.com/blog/sharepoint-javascript-context-development-part-4-the-way-of-the-async-delta-manager/)
* [Андерсон Marc - выполнение JavaScript после MDS (нагрузки повторное)](http://blog.symprogress.com/2013/09/sharepoint-2013-execute-javascript-function-after-mds-load/)
