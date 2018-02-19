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
# <a name="recommendations-for-working-with-css-in-sharepoint-framework-solutions"></a>Рекомендации по работе с CSS в решениях SharePoint Framework

Вы можете использовать CSS, чтобы описать, как должна выглядеть и работать настройка SharePoint Framework. В этой статье описано, как лучше всего использовать возможности SharePoint Framework и с легкостью создавать стили CSS.

## <a name="sharepoint-framework-customizations-are-part-of-the-page"></a>Настройки SharePoint Framework являются частью страницы

Решения SharePoint, созданные по образцу надстройки, изолированы от других элементов на странице. Код может выполняться в iframe как часть надстройки или как иммерсивное приложение, контролирующее всю страницу. В любом случае на него не влияют другие элементы и стили, определенные на странице.

Решения SharePoint Framework являются частью страницы и полностью интегрируются с моделью DOM этой страницы. Хотя это снимает ряд ограничений, связанных с моделью надстройки, ваше решение подвергается риску. Если эта часть страницы не будет явно изолирована, к ней будут применяться все стили CSS, которые есть на странице, что может привести к нежелательным результатам. Чтобы избежать таких рисков, нужно определить стили CSS так, чтобы они не влияли ни на что другое на странице, кроме вашей настройки.

## <a name="organize-css-files-in-your-solution"></a>Организация файлов CSS в решении

Пользовательский интерфейс решений часто состоит из нескольких стандартных блоков. Во многих библиотеках JavaScript эти стандартные блоки называются компонентами. Компонент может быть простым и определять только представление или сложным и включать состояние и другие компоненты. Разделение решения на несколько компонентов позволяет упростить процесс разработки, а также облегчает их тестирование и повторное использование в решении.

Так как компоненты определяют представление, часто возникает потребность в стилях CSS. В идеале компоненты должны быть изолированы, чтобы их можно было использовать отдельно. Поэтому следует хранить стили CSS для конкретного компонента и все другие файлы ресурсов вместе с компонентом. Ниже приведен пример структуры приложения React с несколькими компонентами вместе с их файлами CSS.

```text
todoWebPart\components
                      \todoList
                               \todoList.tsx
                               \todoList.module.scss
                      \todoItem
                               \todoItem.tsx
                               \todoItem.module.scss
```

## <a name="use-sass"></a>Использование SASS

В SharePoint Framework можно использовать как CSS, так и SASS. SASS — это расширенная версия CSS, которая поддерживает переменные, вложение селекторов и примеси — все это упрощает работу со стилями CSS и управление ими в долгосрочной перспективе. 

Полный набор функций см. на [веб-сайте Sass](http://sass-lang.com). Синтаксис CSS полностью совместим с синтаксисом SASS, что очень полезно, если вы еще не работали с SASS раньше и хотите постепенно изучить его возможности.

## <a name="avoid-using-ids-in-markup"></a>Не используйте идентификаторы в разметке

Используя SharePoint Framework, вы создаете настройки, которые пользователи добавляют в SharePoint. Невозможно предугадать, сколько экземпляров конкретной настройки будет открыто на странице. 

Чтобы избежать проблем, всегда следует предполагать наличие нескольких экземпляров настройки на странице. Именно поэтому не следует использовать идентификаторы в разметке. Идентификаторы на странице должны быть уникальными, а добавление двух одинаковых веб-частей на страницу нарушает это условие и может привести к ошибкам.

#### <a name="bad-practice"></a>Не рекомендуется

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

#### <a name="good-practice"></a>Рекомендуется

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

## <a name="use-css-modules-to-avoid-styling-conflicts"></a>Использование CSS-модулей для избежания конфликтов стилей

Решения SharePoint Framework являются частью страницы. Чтобы стили CSS для одного компонента не влияли на другие элементы на странице, нужно определить селекторы CSS таким образом, чтобы они применялись только к модели DOM вашего решения. Делать это вручную утомительно и потенциально подвержено ошибкам, но SharePoint Framework может сделать это для вас автоматически.

Чтобы избежать конфликтов стилей, SharePoint Framework использует [модули CSS](https://github.com/css-modules/css-modules). При сборке проекта цепочка инструментов SharePoint Framework обрабатывает все файлы с расширением **.module.scss**. Для каждого файла SharePoint Framework считывает все селекторы классов и добавляет к ним уникальное хэш-значение. После этого он записывает обновленные селекторы в промежуточные файлы CSS, которые включаются в пакет веб-части.

В продолжение предыдущего примера, предположим, что у вас было два следующих файла SASS:

#### <a name="todolistmodulescss"></a>todoList.module.scss

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

#### <a name="todoitemmodulescss"></a>todoItem.module.scss

```scss
.todoItem {
  padding: 0.5em 1em;

  .text {
    font-size: 0.9em;
  }
}
```

<br/>

После создания проекта в папке **lib** появится два созданных файла CSS, представленных ниже (разрывы строк и отступы добавлены для лучшей читаемости):

#### <a name="todolistmodulecss"></a>todoList.module.css

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

#### <a name="todoitemmodulecss"></a>todoItem.module.css

```css
.todoItem_f7081cc4 {
  padding:.5em 1em
}

.todoItem_f7081cc4 .text_f7081cc4 {
  font-size:.9em
}
```

<br/>

Несмотря на то что в обоих файлах SASS был определен класс **.text**, в созданных файлах CSS к нему добавлены к нему два разных хэша, что делает его уникальным именем класса, характерным для каждого компонента.

Имена классов CSS в модулях CSS генерируются динамически, что делает невозможным непосредственное обращение к ним в коде. Вместо этого при обработке модулей CSS цепочка инструментов SharePoint Framework генерирует файл JavaScript со ссылками на сгенерированные имена классов.

#### <a name="todolistmodulescssjs"></a>todoList.module.scss.js

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

Чтобы использовать сгенерированные имена классов в своем коде, сначала импортируйте стили своего компонента, а затем используйте свойство, указывающее на конкретный класс:

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

Для правильной работы модулей CSS должны выполняться следующие условия:

* Файлы SASS должны иметь расширение **.module.scss**. Если используется расширение **.scss** без **.module**, в ходе сборки отобразится предупреждение. Файл SASS будет транспилирован в промежуточный файл CSS, но имена классов *не будут уникальными*. Расширение .module может не использоваться преднамеренно, когда необходимо переопределить сторонние стили CSS.

* Имена классов CSS должны быть действительными именами переменных JavaScript. Например, они не могут содержать дефисы: `todoList` — правильно, а `todo-list` — неправильно.

* Рекомендуем указывать имена классов в верблюжьем регистре, но это не обязательно.

## <a name="wrap-your-css-styles-in-a-class-named-after-the-component"></a>Упаковка стилей CSS в класс, названный именем компонента

Объединив модули CSS с поддержкой вложения наборов правил SASS, можно упростить стили CSS и убедиться, что они не повлияют на другие элементы на странице.

Упакуйте стили CSS в класс, названный именем компонента, для которого они созданы. Затем назначьте этот класс корневому элементу компонента.

#### <a name="todolistmodulescss"></a>todoList.module.scss

```scss
.todoList {
  a {
    display: block;
  }
}
```

<br/>

#### <a name="todolisttsx"></a>TodoList.tsx

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

После транспиляции файл CSS будет выглядеть примерно так:

```css
.todoList_3e9d35f0 a {
  display: block;
}
```

Так как селектор начинается с уникального имени класса, используемого для компонента, альтернативное представление применяется только к гиперссылкам внутри компонента.

## <a name="handling-of-css-vendor-prefix"></a>Обработка префикса поставщика CSS

В SharePoint Framework не требуются свойства стиля с префиксом поставщика в SASS- и CSS-файлах проекта. Если в поддерживаемых браузерах требуются префиксы, они добавляются после компиляции SASS в CSS автоматически. Этот способ также называется автоматическим добавлением префикса и является фундаментальной составляющей цепочки сборки CSS в SharePoint Framework.

Если веб-часть должна использовать новую модель адаптируемого блока (определяется объявлением `display: flex`), в некоторых старых браузерах на основе WebKit и Internet Explorer требуется определенный префикс поставщика в CSS.

```css
.container{
  display: flex;
}
```

<br/>

В код SASS артефакта SharePoint не требуется включать префиксы поставщиков. Они автоматически добавляются после компиляции SASS в CSS. В итоге получается приведенное ниже объявление CSS.

```css
.container_7e976ae1 {
  display: -webkit-box; // older Safari on MacOS and iOS
  display: -ms-flexbox; // IE 10 - 11
  display: flex;
}
```

<br/>

Удаление уже примененных префиксов не только делает код артефакта проще. Это также делает код более легким для чтения и упрощает его использование в будущем. Кроме того, этот процесс обеспечивает поддержку только тех браузеров, которые совместимы с SharePoint Framework, и защиту от ошибок.

Если веб-часть уже содержит префиксы поставщиков в SASS-файлах, которые больше не требуются, этот процесс автоматически удаляет соответствующие объявления.

В примере ниже используется свойство `border-radius`, для которого не требуются префиксы поставщиков в поддерживаемых системах.

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

Полученная таблица CSS в пакете преобразовывается в приведенный ниже код.

```css
.container_9e54c0b0 {
  border-radius: 7px
}
```

Дополнительные сведения об автоматическом добавлении префиксов см. в документации из репозитория [autoprefixer](https://github.com/postcss/autoprefixer) на сайте GitHub. База данных с описанием этого процесса доступна на сайте [Can I use__?](https://caniuse.com).

## <a name="integrate-office-ui-fabric"></a>Интеграция с Office UI Fabric

Если ваши настройки будут выглядеть и работать как стандартные функции SharePoint и Office 365, пользователям будет удобнее с ними работать. В Office UI Fabric вы найдете набор элементов управления и стилей, при использовании которых ваши настройки будут идеально вписываться в существующий интерфейс. 

Дополнительные сведения об использовании Office UI Fabric в SharePoint Framework см. в [этой статье](./office-ui-fabric-integration.md).

## <a name="use-theme-colors"></a>Использование цветов темы

SharePoint позволяет пользователям выбирать цвет темы для своих сайтов. Тема настройки SharePoint Framework должна соответствовать теме, выбранной пользователями, чтобы настройка выглядела как неотъемлемая часть сайта и излишне не выделялась. 

Так как пользователи выбирают тему на своем сайте, невозможно предугадать, какие цвета вам следует использовать в настройках, но SharePoint Framework может динамично загружать активную цветовую схему автоматически. 

Дополнительные сведения об этой возможности см. в статье [Использование цветов темы в настройках SharePoint Framework](./use-theme-colors-in-your-customizations.md).




