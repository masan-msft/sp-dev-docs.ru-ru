---
title: "Подключение клиентской веб-части к SharePoint (Hello World, часть 2)"
description: "Получите доступ к функциям и данным SharePoint и предоставьте больше интегрированных возможностей для пользователей."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 04cd665f9bb3c09373de297d56a730220be5be78
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="connect-your-client-side-web-part-to-sharepoint-hello-world-part-2"></a>Подключение клиентской веб-части к SharePoint (Hello World, часть 2)

Подключите веб-часть к SharePoint, чтобы получить доступ к функциям и данным SharePoint и предоставить больше интегрированных возможностей для пользователей. В этой статье мы продолжим работу с веб-частью Hello World, создание которой показано в предыдущей статье, [Создание первой веб-части](./build-a-hello-world-web-part.md).

Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=hYrP6D4FaaU&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=3). 

<a href="https://www.youtube.com/watch?v=hYrP6D4FaaU&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=3">
<img src="../../../images/spfx-youtube-tutorial2.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="run-gulp-serve"></a>Запуск команды gulp serve

Убедитесь, что команда `gulp serve` запущена. В противном случае перейдите в каталог проекта **helloworld-webpart** и запустите ее, используя указанные ниже команды.

```
cd helloworld-webpart
gulp serve
```

## <a name="get-access-to-page-context"></a>Получение доступа к контексту страницы

Когда Workbench размещается на локальном компьютере, вам не доступен контекст страницы SharePoint. И все же веб-часть можно проверить различными способами. Например, вы можете сосредоточиться на создании удобной веб-части и использовать фиктивные данные для имитации взаимодействия с SharePoint.

Однако когда Workbench размещается в SharePoint, вы получаете доступ к контексту страницы с различными ключевыми свойствами, такими как:

* название сайта;
* абсолютный URL-адрес сайта;
* URL-адрес относительно веб-сервера;
* имя пользователя для входа.

### <a name="to-get-access-to-the-page-context"></a>Получение доступа к контексту страницы

1. Используйте следующую переменную в своем классе веб-частей:

  ```typescript
  this.context.pageContext
  ```

2. Перейдите в Visual Studio Code (или другую интегрированную среду разработки) и откройте файл **src\webparts\helloWorld\HelloWorldWebPart.ts**.

3. Замените блок кода **innerHTML** в методе **render** на следующий код:

  ```HTML
      this.domElement.innerHTML = `
        <div class="${ styles.helloWorld }">
          <div class="${ styles.container }">
            <div class="${ styles.row }">
              <div class="${ styles.column }">
                <span class="${ styles.title }">Welcome to SharePoint!</span>
                <p class="${ styles.subTitle }">Customize SharePoint experiences using Web Parts.</p>
                <p class="${ styles.description }">${escape(this.properties.description)}</p>
                <p class="${ styles.description }">${escape(this.properties.test)}</p>
                <p class="${ styles.description }">Loading from ${escape(this.context.pageContext.web.title)}</p>
                <a href="https://aka.ms/spfx" class="${ styles.button }">
                  <span class="${ styles.label }">Learn more</span>
                </a>
              </div>
            </div>
          </div>
        </div>`;
  ```

4. Обратите внимание, что для вывода значения переменной в блоке HTML используется `${ }`. Дополнительный HTML `p` используется для отображения `this.context.pageContext.web.title`. Так как эта веб-часть загружается из локальной среды, в заголовке будет указано **Local Workbench**.

5. Сохраните файл. Команда `gulp serve`, запущенная в консоли, определит эту операцию и сделает следующее:

  - выполнит сборку обновленного кода и объединит его в пакет автоматически;
  - обновит страницу локальной версии Workbench (так как код веб-части необходимо перезагрузить).

  > [!NOTE]
  > Поместите окно консоли рядом с окном Visual Studio Code, чтобы видеть, как gulp автоматически выполняет компиляцию при сохранении изменений в Visual Studio Code.

6. В браузере откройте вкладку локальной версии **SharePoint Workbench**. URL-адрес этой вкладки: `https://localhost:4321/temp/workbench.html` (на случай, если вы ее закрыли).

  Веб-часть должна выглядеть следующим образом:

  ![Контекст страницы SharePoint на localhost](../../../images/sp-mock-localhost-wp.png)

7. Перейдите к версии SharePoint Workbench, размещенной в SharePoint. Полный URL-адрес: `https://your-sharepoint-site-url/_layouts/workbench.aspx`. Обратите внимание на то, что на стороне SharePoint Online необходимо обновить страницу, чтобы увидеть внесенные изменения.

  > [!NOTE]
  > Если у вас не установлен сертификат разработчика SPFx, Workbench сообщит вам, что он не загружает скрипты из localhost. Выполните команду `gulp trust-dev-cert` в консоли каталога проекта, чтобы установить сертификат разработчика.

  Теперь, когда веб-части доступен контекст страницы, в ней появится название сайта SharePoint.

  ![Контекст страницы SharePoint на сайте SharePoint](../../../images/sp-lists-spsiteurl-wp.png)

## <a name="define-list-model"></a>Определение модели списка

Чтобы начать работу с данными списка SharePoint, нужна модель списка. Для получения списков нужны две модели. 

1. Откройте Visual Studio Code и перейдите к файлу **src\webparts\helloWorld\HelloWorldWebPart.ts**.

2. Определите следующие модели `interface` над классом **HelloWorldWebPart**:

  ```typescript
  export interface ISPLists {
    value: ISPList[];
  }

  export interface ISPList {
    Title: string;
    Id: string;
  }
  ```

  Интерфейс **ISPList** содержит данные списков SharePoint, к которым мы подключаемся. 

## <a name="retrieve-lists-from-mock-store"></a>Получение списков из фиктивного магазина

Для проверки веб-части в локальной версии Workbench нужен фиктивный магазин, который возвращает фиктивные данные.

### <a name="to-create-a-mock-store"></a>Создание фиктивного магазина

1. Создайте файл **MockHttpClient.ts** в папке **src\webparts\helloWorld**.

2. Скопируйте следующий код в файл **MockHttpClient.ts**:

  ```typescript
  import { ISPList } from './HelloWorldWebPart';

  export default class MockHttpClient  {

      private static _items: ISPList[] = [{ Title: 'Mock List', Id: '1' },
                                          { Title: 'Mock List 2', Id: '2' },
                                          { Title: 'Mock List 3', Id: '3' }];
      
      public static get(): Promise<ISPList[]> {
      return new Promise<ISPList[]>((resolve) => {
              resolve(MockHttpClient._items);
          });
      }
  }
  ```

  Вот что нужно знать о коде:

  - Так как в файле **HelloWorldWebPart.ts** несколько операций экспорта, операция импорта указана с помощью скобок `{ }`. В этом случае требуется только модель данных `ISPList`.
  - При импорте из модуля по умолчанию (в данном случае — **HelloWorldWebPart**) не нужно вводить расширение файла. 
  - Класс **MockHttpClient** экспортируется как модуль по умолчанию, чтобы его можно было импортировать в другие файлы.
  - Он создает исходный фиктивный массив `ISPList` и выходные данные.

3. Сохраните файл.

Теперь вы можете использовать класс **MockHttpClient** в классе **HelloWorldWebPart**. Сначала нужно импортировать модуль **MockHttpClient**.

### <a name="to-import-the-mockhttpclient-module"></a>Импорт модуля **MockHttpClient**

1. Откройте файл **HelloWorldWebPart.ts**.

2. Скопируйте приведенный ниже код и вставьте его под оператором `import * as strings from 'HelloWorldWebPartStrings';`.

  ```typescript
  import MockHttpClient from './MockHttpClient';
  ```
 
3. Добавьте приведенный ниже частный метод, имитирующий извлечение списков, в класс **HelloWorldWebPart**.

  ```typescript
    private _getMockListData(): Promise<ISPLists> {
      return MockHttpClient.get()
        .then((data: ISPList[]) => {
          var listData: ISPLists = { value: data };
          return listData;
        }) as Promise<ISPLists>;
    }
  ```

4. Сохраните файл.

## <a name="retrieve-lists-from-sharepoint-site"></a>Получение списков с сайта SharePoint

Далее нужно получить списки с текущего сайта. Чтобы получить списки с сайта `https://yourtenantprefix.sharepoint.com/_api/web/lists`, нужно использовать REST API SharePoint.

Платформа SharePoint Framework включает вспомогательный класс **spHttpClient** для выполнения запросов REST API к SharePoint. Он добавляет заголовки, управляет дайджестом, необходимым для записи, и собирает данные телеметрии, которые помогают службе отслеживать производительность приложения.

### <a name="to-use-this-helper-class-import-them-from-the-microsoftsp-http-module"></a>Чтобы использовать этот вспомогательный класс, импортируйте его из модуля @microsoft/sp-http

1. Прокрутите к началу файла **HelloWorldWebPart.ts**. 

2. Скопируйте приведенный ниже код и вставьте его под оператором `import MockHttpClient from './MockHttpClient';`.

  ```typescript
  import {
    SPHttpClient,
    SPHttpClientResponse   
  } from '@microsoft/sp-http';
  ```

3. Добавьте приведенный ниже частный метод для получения списков из SharePoint в класс **HelloWorldWebPart**.

  ```typescript
  private _getListData(): Promise<ISPLists> {
    return this.context.spHttpClient.get(this.context.pageContext.web.absoluteUrl + `/_api/web/lists?$filter=Hidden eq false`, SPHttpClient.configurations.v1)
      .then((response: SPHttpClientResponse) => {
        return response.json();
      });
  }
  ```

  Этот метод использует вспомогательный класс **spHttpClient** и отправляет запрос `get`. Он использует модель **ISPLists**, а также применяет фильтр, чтобы не получать скрытые списки.

4. Сохраните файл. 

5. Перейдите в окно консоли, в котором запущена команда `gulp serve`, и проверьте наличие ошибок. Если gulp сообщит об ошибках, их нужно исправить.

## <a name="add-new-styles"></a>Добавление новых стилей

Платформа SharePoint Framework использует [Sass](http://sass-lang.com/) в качестве препроцессора CSS и [синтаксис SCSS](http://sass-lang.com/documentation/file.SCSS_FOR_SASS_USERS.html), который полностью совместим со стандартным синтаксисом CSS. Sass расширяет язык CSS и позволяет использовать такие возможности, как переменные, вложенные правила и встроенные операции импорта, для упорядочения и создания эффективных таблиц стилей для веб-частей. Платформа SharePoint Framework предусматривает наличие компилятора SCSS, который преобразует файлы Sass в обычные CSS-файлы, а также типизированной версии для использования во время разработки.

### <a name="to-add-new-styles"></a>Добавление новых стилей

1. Откройте **HelloWorld.module.scss**. В этом SCSS-файле можно задавать стили.

  По умолчанию стили действуют на уровне веб-части. Это видно, так как стили задаются в разделе **.helloWorld**.

2. Добавьте следующие стили после стиля `.button` в главном разделе стилей `.helloWorld`:

  ```css
  .list {
    color: #333333;
    font-family: 'Segoe UI Regular WestEuropean', 'Segoe UI', Tahoma, Arial, sans-serif;
    font-size: 14px;
    font-weight: normal;
    box-sizing: border-box;
    margin: 10;
    padding: 10;
    line-height: 50px;
    list-style-type: none;
    box-shadow: 0 4px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
  }

  .listItem {
    color: #333333;
    vertical-align: center;
    font-family: 'Segoe UI Regular WestEuropean', 'Segoe UI', Tahoma, Arial, sans-serif;
    font-size: 14px;
    font-weight: normal;
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    box-shadow: none;
    *zoom: 1;
    padding: 9px 28px 3px;
    position: relative;
  }
  ``` 

3. Сохраните файл.

  Средство gulp перестраивает код в консоли, как только вы сохраняете файл. При этом создаются соответствующие определения типов в файле **HelloWorld.module.scss.ts**. После компиляции для TypeScript вы можете импортировать эти стили и ссылаться на них в коде веб-части.

  Это видно в методе **render** веб-части:

  ```html
  <div class="${styles.row}">
  ```

## <a name="render-lists-information"></a>Отрисовка данных списков

Перейдите к классу **HelloWorldWebPart**.

SharePoint Workbench можно использовать для проверки веб-частей в локальной среде и на сайте SharePoint. Платформа SharePoint Framework показывает, в какой среде запущена веб-часть, с помощью модуля **EnvironmentType**. 

### <a name="to-use-the-environmenttype-module"></a>Использование модуля EnvironmentType

1. Импортируйте модули **Environment** и **EnvironmentType** из пакета **@microsoft/sp-core-library**. Добавьте в раздел **import** вверху, как показано в следующем фрагменте кода:

  ```typescript
  import {
    Environment,
    EnvironmentType
  } from '@microsoft/sp-core-library';
  ```

2. Добавьте следующий частный метод в класс **HelloWorldWebPart** для вызова соответствующих методов и получения данных списков:

  ```typescript
    private _renderListAsync(): void {
      // Local environment
      if (Environment.type === EnvironmentType.Local) {
        this._getMockListData().then((response) => {
          this._renderList(response.value);
        });
      }
      else if (Environment.type == EnvironmentType.SharePoint || 
                Environment.type == EnvironmentType.ClassicSharePoint) {
        this._getListData()
          .then((response) => {
            this._renderList(response.value);
          });
      }
    }
  ```

  Вот что нужно знать о hostType в методе **_renderListAsync**:

  - Свойство `Environment.type` поможет вам проверить, в какой среде вы находитесь (локальной или SharePoint).
  - В зависимости от того, где размещается Workbench, вызывается нужный метод.

3. Сохраните файл.

  Теперь данные списков нужно отрисовать при помощи значения, полученного из REST API.

4. Добавьте следующий метод private в класс **HelloWorldWebPart**:

  ```typescript
    private _renderList(items: ISPList[]): void {
      let html: string = '';
      items.forEach((item: ISPList) => {
        html += `
      <ul class="${styles.list}">
        <li class="${styles.listItem}">
          <span class="ms-font-l">${item.Title}</span>
        </li>
      </ul>`;
      });

      const listContainer: Element = this.domElement.querySelector('#spListContainer');
      listContainer.innerHTML = html;
    }
  ```

  Предыдущий метод ссылается на новые стили CSS, добавленные с помощью переменной **styles**. 

5. Сохраните файл.


## <a name="retrieve-list-data"></a>Получение данных списков

1. Замените код в методе **render** следующим кодом:

  ```typescript
      this.domElement.innerHTML = `
        <div class="${ styles.helloWorld }">
          <div class="${ styles.container }">
            <div class="${ styles.row }">
              <div class="${ styles.column }">
                <span class="${ styles.title }">Welcome to SharePoint!</span>
                <p class="${ styles.subTitle }">Customize SharePoint experiences using Web Parts.</p>
                <p class="${ styles.description }">${escape(this.properties.description)}</p>
                <p class="${ styles.description }">${escape(this.properties.test)}</p>
                <p class="${ styles.description }">Loading from ${escape(this.context.pageContext.web.title)}</p>
                <a href="https://aka.ms/spfx" class="${ styles.button }">
                  <span class="${ styles.label }">Learn more</span>
                </a>
              </div>
            </div>
            <div id="spListContainer" />
          </div>
        </div>`;

        this._renderListAsync();
  ```

2. Сохраните файл.

  В окне консоли вы заметите, что `gulp serve` перестраивает код. Убедитесь, что нет ошибок.

3. Перейдите в локальную версию Workbench и добавьте веб-часть HelloWorld.

  Должны появиться фиктивные данные.

  ![Отрисовка данных списков из localhost](../../../images/sp-lists-render-localhost.png)

4. Перейдите в версию Workbench, размещенную в SharePoint. Обновите страницу и добавьте веб-часть HelloWorld.

  Должны появиться списки с текущего сайта.

  ![Отрисовка данных списков из SharePoint](../../../images/sp-lists-render-spsite.png)

5. Теперь вы можете остановить работу сервера. Перейдите в консоль и остановите команду `gulp serve`. Нажмите клавиши Ctrl+C, чтобы завершить задачу gulp.

## <a name="next-steps"></a>Дальнейшие действия

Поздравляем: вы подключили веб-часть к данным списков SharePoint! 

Из следующей статьи, которая называется [Развертывание веб-части на странице SharePoint](./serve-your-web-part-in-a-sharepoint-page.md), вы узнаете, как развернуть и просмотреть веб-часть Hello World на странице SharePoint.

> [!NOTE]
> Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues). Заранее спасибо!