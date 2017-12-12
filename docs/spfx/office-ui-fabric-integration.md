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
# <a name="using-office-ui-fabric-core-and-fabric-react-in-sharepoint-framework"></a>Использование Office UI Fabric Core и Fabric React в SharePoint Framework

Office UI Fabric — это официальная клиентская платформа для создания интерфейсов в Office 365 и SharePoint. SharePoint обеспечивает полную интеграцию с Fabric, благодаря которой корпорация Майкрософт может предоставлять надежный и согласованный язык дизайна в различных решениях на основе SharePoint, таких как современные сайты групп, страницы и списки. Кроме того, платформа Office UI Fabric доступна разработчикам в SharePoint Framework при создании пользовательских решений SharePoint.

## <a name="summary"></a>Сводка

Корпорация Майкрософт использует Fabric Core и Fabric React в SharePoint. Она регулярно выпускает обновления для SharePoint Online, при установке которых также могут обновиться ваши версии Fabric Core и Fabric React. Возможны конфликты этих обновлений со сторонними клиентскими решениями, созданными с помощью предыдущих версий Fabric Core и Fabric React. В результате этого в таких модификациях могут возникать исключения. Основная причина таких сбоев — использование **глобальных стилей CSS** в обеих библиотеках Fabric. Таких конфликтов следует избегать любой ценой. 

> Трудности с глобальными стилями CSS хорошо описаны в следующей презентации на примере React и JSS: [React CSS в JS](https://speakerdeck.com/vjeux/react-css-in-js).

Одно из главных препятствий для обеспечения надежности — использование **глобальных стилей CSS**. Это гарантирует, что вместо глобальных имен классов в разметке HTML будут использоваться примеси и переменные Fabric Core в файле объявлений SASS. При этом объявления SASS для Fabric Core импортируются из файла SASS, после чего переменные и примеси используются надлежащим образом. 

## <a name="goals"></a>Цели

Цель SharePoint Framework — помочь корпорации Майкрософт и ее клиентам создавать функциональные, привлекательные и согласованные решения на основе SharePoint. Достижению этих целей способствуют основные принципы разработки.

* Удобство и надежность для пользователей при использовании Fabric Core и Fabric React в решениях.
* Корпорация Майкрософт должна развертывать обновленные решения, использующие обновленные версии Fabric Core и Fabric React, в SharePoint без конфликтов с решениями клиента.
* Пользователи должны иметь возможность настраивать и переопределять стили, оформление и компоненты в соответствии с потребностями решения.

Office UI Fabric состоит из двух частей, доступных разработчикам:

* [Office UI Fabric Core](http://dev.office.com/fabric)

  Набор, включающий основные стили, оформление, адаптируемую сетку, анимацию, значки и другие стандартные блоки общего языка дизайна.

* [Office UI Fabric React](http://dev.office.com/fabric#/components)

  Набор компонентов React, основанных на языке дизайна Fabric, для использования в проектах на основе React.

## <a name="spfx-fabric-core-package"></a>Пакет SPFx Fabric Core

Пакет npm с SPFx Fabric Core (sp-office-ui-fabric-core) содержит часть поддерживаемых стилей Fabric Core, которые можно с уверенностью использовать в компоненте SharePoint Framework. 

В пакете поддерживаются следующие основные стили:
- шрифтовое оформление;
- макеты;
- цвета;
- темы;
- локализация.

В нем пока что не поддерживаются следующие элементы:
- анимация;
- значки.

Начиная с версии 1.3.4 генератора Yeoman для SharePoint Framework стандартные шаблоны проектов (веб-частей и расширений) включают новый пакет sp-office-ui-fabric-core и используют основные стили из пакета, а не глобальные стили CSS. 

### <a name="updating-existing-projects"></a>Обновление существующих проектов

Чтобы использовать пакет SPFx Fabric Core в имеющемся проекте, установите пакет в качестве зависимости для разработки:

```
npm install @microsoft/sp-office-ui-fabric-core --save-dev
```

После установки можно импортировать объявления SASS для Fabric Core из файла определений SASS, а затем использовать примеси и переменные, как описано в приведенном ниже разделе. 

### <a name="using-fabric-core-styles"></a>Использование стилей Fabric Core

Чтобы использовать стили Fabric Core, для начала необходимо импортировать объявления SPFabricCore из файла SASS.

> Примечание. Убедитесь, что установлен пакет npm sp-office-ui-fabric-core.

```css
@import '~@microsoft/sp-office-ui-fabric-core/dist/sass/SPFabricCore.scss';
```

Теперь вы можете использовать основные стили в качестве примесей и переменных.

```css
.row {
    @include ms-Grid-row;
    @include ms-fontColor-white;
    background-color: $ms-color-themeDark;
    padding: 20px;
  }
 ``` 

## <a name="using-office-ui-fabric-react"></a>Использование Office UI Fabric React

Рекомендуем установить последнюю версию пакета Office UI Fabric React и добавить в пакет явную зависимость от этой конкретной версии. В пакет будут включена компоненты, используемые в решении SPFx — веб-части или расширении (в зависимости от того, для каких целей используются компоненты Fabric React). 

> Обратите внимание, что Fabric React версий 2.x и ниже не поддерживается в SharePoint Framework.

Установив пакет Fabric React, вы можете импортировать из него необходимые компоненты.

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

Пакет Fabric React включает поддерживаемые стили Fabric Core, используемые в компонентах Fabric React. Рекомендуем импортировать стили Fabric Core из пакета Fabric React, а не sp-office-ui-fabric-core, чтобы обеспечить использование подходящих стилей в компоненте. 

Так как пакет sp-office-ui-fabric-core уже установлен в решении генератором Yeoman, рекомендуем удалить этот пакет, если вы решите использовать компоненты Fabric и уменьшить размер пакета компонентов.

```
npm uninstall @microsoft/sp-office-ui-fabric-core --save-dev
```

Затем вы можете импортировать основные стили из объявлений SASS, доступных в пакете Fabric React.

```css
@import '~office-ui-fabric-react/dist/sass/References.scss';
```

### <a name="understanding-this-approach-and-its-shortcomings"></a>Общие сведения об этом подходе и его недостатках

Компоненты Fabric в решении привязаны к установленной у вас версии Fabric React. Чтобы получить новые компоненты (если они доступны в более новой версии пакета), необходимо обновить пакет Fabric React. Так как компоненты Fabric включены в пакет компонентов, его размер может увеличиться. Однако это единственный официально поддерживаемый подход при использовании Office UI Fabric React в решениях SharePoint Framework.


## <a name="additional-details-on-the-css-challenge-with-office-ui-fabric"></a>Дополнительные сведения о трудностях с CSS в Office UI Fabric
Представленные ниже понятия и ссылки раскрывают суть проблем с использованием Office UI Fabric в контексте клиентских веб-частей. 

**Глобальные стили CSS** и как избегать их использования любой ценой: это серьезная проблема. На данный момент библиотеки Fabric Core и Fabric React содержат глобальные стили. Отсутствие встроенных в браузеры решений для управления областями стилей делает это очень трудной задачей.
  
  - [Области CSS](https://developer.mozilla.org/ru-RU/docs/Web/CSS/:scope) находятся на ранней стадии рассмотрения. 
  - Элементы IFrame плохо подходят для изолирования стилей.
  - [Веб-компоненты](https://developer.mozilla.org/ru-RU/docs/Web/Web_Components) — еще один стандарт, который включает стили с ограниченной областью действия, но пока только обсуждается.
  - В [этом](https://speakerdeck.com/vjeux/react-css-in-js) обсуждении хорошо раскрыта суть проблемы. В Интернете есть множество другой документации, посвященной решениям проблемы с глобальными пространствами имен.
 
**[Специфичность CSS](https://developer.mozilla.org/ru-RU/docs/Web/CSS/Specificity)** и как она связана с веб-интерфейсами. Стили с большей специфичностью переопределяют стили с меньшей специфичностью. Но самое важное — понять, как применяются правила специфичности. Общий порядок приоритетов (по убыванию) выглядит так:
  - Атрибут стиля (например, `style="background:red;"`)
  - Селекторы идентификаторов (например, `#myDiv { }`)
  - Селекторы классов (например, `.myCssClass{}`), селекторы атрибутов (например, `[type="radio"]`) и псевдоклассы (например, `:hover`)
  - Селекторы типов (например, `h1`)

***Порядок загрузки***: если к элементу применяются два класса с одинаковой специфичностью, предпочтение отдается классу, загруженному позже. Как показано в представленном ниже коде, кнопка будет красной. Если изменить порядок тегов стиля, она станет зеленой. Это важное понятие. При его неправильном использовании пользовательский интерфейс начинает зависеть от порядка загрузки, то есть становится несогласованным.

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

## <a name="other-approaches-considered-and-discarded"></a>Другие подходы, которые были рассмотрены и отклонены
Ниже представлены дополнительные сведения о других подходах, которые были рассмотрены, но отклонены, так как они не соответствовали ключевым целям и не позволяли разработчикам безопасно использовать стили Office UI Fabric.

**Office UI Fabric Core**

Разработчику веб-части не требовалось бы выполнять никаких явных действий, чтобы определения областей работали. Мы планировали решить эту проблему с помощью специфичности CSS и селектора потомков. Разработчики Fabric Core собирались выпустить несколько копий CSS-файла Fabric Core, например `fabric-6.css`, `fabric-6-scoped.css`, `fabric-6.0.0.css` и `fabric-6.0.0-scoped.css`.

Все стили в CSS-файлах с ограниченной областью действия были бы включены в селектор потомков, например `"ms-Fabric-core--v6 ms-Icon--List"`. Во время компиляции инструменты получали бы версию Office UI Fabric Core, с помощью которой была создана веб-часть. Это могла быть версия, входящая в состав SPFx. Кроме того, разработчики веб-частей могли бы явно указывать зависимость от определенной версии Office UI Fabric Core в файле **package.json**.

Разделителю веб-части была бы назначена эта область действия, т. е. `<div data-sp-webpart class="ms-Fabric-core--v6">`. Платформа загружала бы определенную основную версию CSS-файла с областью действия на уровне Fabric Core. Если веб-часть была создана с помощью CSS-файла Fabric Core версии 6.0.0, платформа скачивала бы файл `fabric-6-scoped.css` во время загрузки веб-части.

Остальная часть страницы содержала бы стили Office UI Fabric Core с неограниченной областью действия. Таким образом, согласно правилам специфичности CSS внутри разделителя веб-части имели бы приоритет стили CSS с ограниченной областью действия. Веб-часть и ее содержимое были бы адаптированы к определенной версии Office UI Fabric Core, выбранной разработчиком.

**Переопределение** стилей Fabric Core не поддерживалось.  

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

После тщательного анализа этой стратегии было принято решение, что у подхода с использованием селектора потомков есть два серьезных недостатка, не позволяющих создать отказоустойчивую веб-часть.

**Отсутствие надежной поддержки вложения**. Этот подход работает, только если страница и веб-части Майкрософт используют версию Office UI Fabric Core (т. е. `ms-Icon--List`) с неограниченной областью действия, а сторонние веб-части — только CSS Office UI Fabric Core с ограниченной областью действия, как описано выше. Причина заключается в том, что стиль CSS с ограниченной областью действия, примененный к веб-части, переопределяет CSS с неограниченной областью действия на странице. Обратите внимание: как описывалось ранее, если специфичность двух классов CSS совпадает, то предпочтение отдается классу, загруженному позже. Следовательно, для обеспечения согласованности интерфейса важно, чтобы специфичность класса CSS с ограниченной областью действия была выше.

Более того, несколько расширений, вложенных друг в друга, не могут использовать разные версии Fabric Core. Например, в приведенном ниже примере применяется только `ms-Fabric-core--v6`.

```HTML
<div className={css('ms-Fabric-core--v6')}>
  { // Rest of the web part UI }
    { // inside of this SPExtension trying to use different Fabric core version does not work }
    <div className={css('ms-Fabric-core--v8')}>
    </div>
</div>
```

Ниже представлен более простой пример, иллюстрирующий эту проблему.

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

**Утечки из неограниченных классов** — еще одна проблема с селекторами потомков. Обратите внимание, что в приведенном выше примере стили высоты и ширины из неограниченного класса myButton применяются ко всем кнопкам. Это означает, что изменение этого стиля может случайно сделать неработоспособным код HTML, в котором используется разметка с ограниченной областью действия. Допустим, по какой-то причине на уровне приложения мы меняем высоту в классе myButton на 0 пикселей. В результате во всех сторонних веб-частях, использующих класс myButton, будет задана высота в 0 пикселей, что отрицательно скажется на пользовательском интерфейсе.


