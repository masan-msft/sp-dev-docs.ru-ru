---
title: "Подключение клиентской веб-части к SharePoint (Hello world, часть 2)"
ms.date: 12/05/2017
ms.prod: sharepoint
ms.openlocfilehash: 50ba50db6da70ab271d61db1c8f894fd091270c2
ms.sourcegitcommit: 1f752afb40ff133e2fae14337e09392cc5d9d181
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/08/2017
---
# <a name="connect-your-client-side-web-part-to-sharepoint-hello-world-part-2"></a><span data-ttu-id="9d489-102">Подключение клиентской веб-части к SharePoint (Hello world, часть 2)</span><span class="sxs-lookup"><span data-stu-id="9d489-102">Connect your client-side web part to SharePoint (Hello world part 2)</span></span>

<span data-ttu-id="9d489-103">Подключите веб-часть к SharePoint для доступа к функциям и данным SharePoint, а также более интегрированного процесса работы для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="9d489-103">Connect your web part to SharePoint to access functionality and data in SharePoint and provide a more integrated experience for end users.</span></span> <span data-ttu-id="9d489-104">В этой статье мы продолжим работу с веб-частью Hello world, созданной в предыдущей статье [Создание первой веб-части](./build-a-hello-world-web-part.md).</span><span class="sxs-lookup"><span data-stu-id="9d489-104">This article continues building the hello world web part built in the previous article [Build your first web part](./build-a-hello-world-web-part.md).</span></span>

<span data-ttu-id="9d489-105">Указанные ниже действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=hYrP6D4FaaU&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=3).</span><span class="sxs-lookup"><span data-stu-id="9d489-105">You can also follow follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=hYrP6D4FaaU&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=3).</span></span> 

<a href="https://www.youtube.com/watch?v=hYrP6D4FaaU&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=3">
<img src="../../../images/spfx-youtube-tutorial2.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="run-gulp-serve"></a><span data-ttu-id="9d489-106">Запуск команды gulp serve</span><span class="sxs-lookup"><span data-stu-id="9d489-106">Run gulp serve</span></span>

<span data-ttu-id="9d489-107">Убедитесь, что команда `gulp serve` запущена.</span><span class="sxs-lookup"><span data-stu-id="9d489-107">Make sure you have the `gulp serve` command running.</span></span> <span data-ttu-id="9d489-108">В противном случае перейдите в каталог проекта **helloworld-webpart** и запустите ее с помощью указанных ниже команд.</span><span class="sxs-lookup"><span data-stu-id="9d489-108">If it is not already running, go to the **helloworld-webpart** project directory and run it using the following commands.</span></span>

```
cd helloworld-webpart
gulp serve
```

## <a name="get-access-to-page-context"></a><span data-ttu-id="9d489-109">Доступ к контексту страницы</span><span class="sxs-lookup"><span data-stu-id="9d489-109">Get access to page context</span></span>

<span data-ttu-id="9d489-p103">Когда рабочая область размещается на локальном компьютере, вам не доступен контекст страницы SharePoint. И все же веб-часть можно проверить различными способами. Например, вы можете сосредоточиться на пользовательском интерфейсе веб-части и использовать фиктивные данные для имитации взаимодействия с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d489-p103">When the workbench is hosted locally, you do not have the SharePoint page context. You can still test your web part in many different ways. For example, you can concentrate on building the web part's UX and use mock data to simulate SharePoint interaction when you don't have the SharePoint context.</span></span>

<span data-ttu-id="9d489-113">Но когда рабочая область размещается в SharePoint, вы получаете доступ к контексту страницы с различными ключевыми свойствами, такими как:</span><span class="sxs-lookup"><span data-stu-id="9d489-113">However, when the workbench is hosted in SharePoint, you get access to the page context which provides various key properties, such as:</span></span>

* <span data-ttu-id="9d489-114">название сайта;</span><span class="sxs-lookup"><span data-stu-id="9d489-114">Web title</span></span>
* <span data-ttu-id="9d489-115">абсолютный URL-адрес сайта;</span><span class="sxs-lookup"><span data-stu-id="9d489-115">Web absolute URL</span></span>
* <span data-ttu-id="9d489-116">относительный URL-адрес веб-сервера;</span><span class="sxs-lookup"><span data-stu-id="9d489-116">Web server-relative URL</span></span>
* <span data-ttu-id="9d489-117">имя пользователя для входа.</span><span class="sxs-lookup"><span data-stu-id="9d489-117">User login name</span></span>

<span data-ttu-id="9d489-118">Доступ к контексту страницы можно получить с помощью следующей переменной в классе веб-части:</span><span class="sxs-lookup"><span data-stu-id="9d489-118">You can get access to the page context using the following variable in your web part class:</span></span>

```ts
this.context.pageContext
```

<span data-ttu-id="9d489-119">Перейдите в Visual Studio Code (или другую интегрированную среду разработки) и откройте файл **src\webparts\helloWorld\HelloWorldWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="9d489-119">Switch to Visual Studio code (or your preferred IDE) and open **src\webparts\helloWorld\HelloWorldWebPart.ts**.</span></span>

<span data-ttu-id="9d489-120">Замените блок кода **innerHTML** в методе **render** на следующий код:</span><span class="sxs-lookup"><span data-stu-id="9d489-120">Inside the **render** method, replace the **innerHTML** code block with the following code:</span></span>

```ts
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

<span data-ttu-id="9d489-121">Обратите внимание, что для вывода значения переменной в блоке HTML используется `${ }`.</span><span class="sxs-lookup"><span data-stu-id="9d489-121">Notice how `${ }` is used to output the variable's value in the HTML block.</span></span> <span data-ttu-id="9d489-122">Дополнительный HTML `p` используется для отображения `this.context.pageContext.web.title`.</span><span class="sxs-lookup"><span data-stu-id="9d489-122">An extra HTML `p` is used to display `this.context.pageContext.web.title`.</span></span> <span data-ttu-id="9d489-123">Так как эта веб-часть загружается из локальной среды, в заголовке будет указано **Локальная рабочая область**.</span><span class="sxs-lookup"><span data-stu-id="9d489-123">Since this web part loads from the local environment, the title will be **Local Workbench**.</span></span>

<span data-ttu-id="9d489-124">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="9d489-124">Save the file.</span></span> <span data-ttu-id="9d489-125">Команда `gulp serve`, запущенная в консоли, определит эту операцию и:</span><span class="sxs-lookup"><span data-stu-id="9d489-125">The `gulp serve` running in your console will detect this save operation and:</span></span>

* <span data-ttu-id="9d489-126">выполнит сборку обновленного кода и объединит его в пакет автоматически;</span><span class="sxs-lookup"><span data-stu-id="9d489-126">Build and bundle the updated code automatically.</span></span>
* <span data-ttu-id="9d489-127">Обновите страницу локальной рабочей области (так как код веб-части необходимо перезагрузить).</span><span class="sxs-lookup"><span data-stu-id="9d489-127">Refresh your local workbench page (as the web part code needs to be reloaded).</span></span>

> [!NOTE]
> <span data-ttu-id="9d489-128">Поместите окно консоли рядом с окном VS Code, чтобы видеть, как gulp автоматически выполняет компиляцию при сохранении изменений в VS Code.</span><span class="sxs-lookup"><span data-stu-id="9d489-128">Keep the console window and VS Code side by side to see gulp automatically compile as you save changes in VS Code.</span></span>

<span data-ttu-id="9d489-129">В браузере откройте вкладку локальной рабочей области SharePoint Workbench. URL-адрес этой вкладки: `https://localhost:4321/temp/workbench.html` (на случай, если вы ее закрыли).</span><span class="sxs-lookup"><span data-stu-id="9d489-129">In your browser, switch to the local SharePoint Workbench tab. If you have already closed the tab, the URL is `https://localhost:4321/temp/workbench.html`.</span></span>

<span data-ttu-id="9d489-130">Веб-часть должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9d489-130">You should see the following in the web part:</span></span>

![Контекст страницы SharePoint на localhost](../../../images/sp-mock-localhost-wp.png)

<span data-ttu-id="9d489-132">Теперь перейдите к рабочей области SharePoint Workbench, размещенной в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d489-132">Now, navigate to the SharePoint Workbench hosted in SharePoint.</span></span> <span data-ttu-id="9d489-133">Полный URL-адрес: `https://your-sharepoint-site-url/_layouts/workbench.aspx`.</span><span class="sxs-lookup"><span data-stu-id="9d489-133">The full URL is `https://your-sharepoint-site-url/_layouts/workbench.aspx`.</span></span> <span data-ttu-id="9d489-134">Обратите внимание, что на стороне SharePoint Online необходимо обновить страницу, чтобы увидеть внесенные изменения.</span><span class="sxs-lookup"><span data-stu-id="9d489-134">Notice that in the SharePoint Online side, you'll need to refresh the page to see the changes.</span></span>

> [!NOTE]
> <span data-ttu-id="9d489-135">Если у вас не установлен сертификат разработчика SPFx, рабочая область сообщит вам, что она не загружает сценарии из localhost.</span><span class="sxs-lookup"><span data-stu-id="9d489-135">If you do not have the SPFx developer certificate installed, then Workbench will notify you that it is configured not to load scripts from localhost.</span></span> <span data-ttu-id="9d489-136">Выполните команду `gulp trust-dev-cert` в консоли каталога проекта, чтобы установить сертификат разработчика.</span><span class="sxs-lookup"><span data-stu-id="9d489-136">Execute `gulp trust-dev-cert` command in your project directory console to install the developer certificate.</span></span>

<span data-ttu-id="9d489-137">Теперь, когда веб-части доступен контекст страницы, в ней появится название сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d489-137">You should now see your SharePoint site title in the web part now that page context is available to the web part.</span></span>

![Контекст страницы SharePoint на сайте SharePoint](../../../images/sp-lists-spsiteurl-wp.png)

## <a name="define-list-model"></a><span data-ttu-id="9d489-139">Определение модели списка</span><span class="sxs-lookup"><span data-stu-id="9d489-139">Define list model</span></span>
<span data-ttu-id="9d489-p108">Чтобы начать работу с данными списка SharePoint, нужна модель списка. Для получения списков нужны две модели.</span><span class="sxs-lookup"><span data-stu-id="9d489-p108">You need a list model to start working with SharePoint list data. To retrieve the lists, you need two models.</span></span> 

<span data-ttu-id="9d489-142">Откройте Visual Studio Code и перейдите к файлу **src\webparts\helloWorld\HelloWorldWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="9d489-142">Switch to Visual Studio Code and go to **src\webparts\helloWorld\HelloWorldWebPart.ts**.</span></span>

<span data-ttu-id="9d489-143">Определите следующие модели `interface` над классом **HelloWorldWebPart**:</span><span class="sxs-lookup"><span data-stu-id="9d489-143">Define the following `interface` models just above the **HelloWorldWebPart** class:</span></span>

```ts
export interface ISPLists {
    value: ISPList[];
}

export interface ISPList {
    Title: string;
    Id: string;
}
```

<span data-ttu-id="9d489-144">Интерфейс **ISPList** содержит данные списков SharePoint, к которым мы подключаемся.</span><span class="sxs-lookup"><span data-stu-id="9d489-144">The **ISPList** interface holds the SharePoint list information we are connecting to.</span></span> 

## <a name="retrieve-lists-from-mock-store"></a><span data-ttu-id="9d489-145">Получение списков из фиктивного магазина</span><span class="sxs-lookup"><span data-stu-id="9d489-145">Retrieve lists from mock store</span></span>

<span data-ttu-id="9d489-146">Для проверки веб-части в локальной рабочей области нужен фиктивный магазин, который возвращает фиктивные данные.</span><span class="sxs-lookup"><span data-stu-id="9d489-146">To test in the local workbench you will need a mock store that returns mock data.</span></span>

<span data-ttu-id="9d489-147">Создайте файл **MockHttpClient.ts** в папке **src\webparts\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="9d489-147">Create a new file inside the **src\webparts\helloWorld** folder named **MockHttpClient.ts**.</span></span>

<span data-ttu-id="9d489-148">Скопируйте следующий код в файл **MockHttpClient.ts**:</span><span class="sxs-lookup"><span data-stu-id="9d489-148">Copy the following code into **MockHttpClient.ts**:</span></span>

```ts
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

<span data-ttu-id="9d489-149">Вот что нужно знать о коде:</span><span class="sxs-lookup"><span data-stu-id="9d489-149">Things to note about the code:</span></span>

* <span data-ttu-id="9d489-150">Так как в файле **HelloWorldWebPart.ts** несколько операций экспорта, операция импорта указана с помощью скобок `{ }`.</span><span class="sxs-lookup"><span data-stu-id="9d489-150">Because there are multiple exports in **HelloWorldWebPart.ts** the specific one to import is specified using `{ }`.</span></span> <span data-ttu-id="9d489-151">В этом случае требуется только модель данных `ISPList`.</span><span class="sxs-lookup"><span data-stu-id="9d489-151">In this case, only the data model `ISPList` is required.</span></span>
* <span data-ttu-id="9d489-152">При импорте из модуля по умолчанию (в данном случае — **HelloWorldWebPart**) не нужно вводить расширение файла.</span><span class="sxs-lookup"><span data-stu-id="9d489-152">You do not need to type the file extension when importing from the default module which in this case is **HelloWorldWebPart**.</span></span> 
* <span data-ttu-id="9d489-153">Он экспортирует класс **MockHttpClient** как модуль по умолчанию, чтобы его можно было импортировать в другие файлы.</span><span class="sxs-lookup"><span data-stu-id="9d489-153">It exports the **MockHttpClient** class as a default module so that it can be imported in other files.</span></span>
* <span data-ttu-id="9d489-154">Он создает исходный фиктивный массив `ISPList` и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="9d489-154">It builds the initial `ISPList` mock array and returns.</span></span>

<span data-ttu-id="9d489-155">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="9d489-155">Save the file.</span></span>

<span data-ttu-id="9d489-156">Теперь вы можете использовать класс **MockHttpClient** в классе **HelloWorldWebPart**.</span><span class="sxs-lookup"><span data-stu-id="9d489-156">You can now use the **MockHttpClient** class in the **HelloWorldWebPart** class.</span></span> <span data-ttu-id="9d489-157">Сначала нужно импортировать модуль **MockHttpClient**.</span><span class="sxs-lookup"><span data-stu-id="9d489-157">You first need to import the **MockHttpClient** module.</span></span>

<span data-ttu-id="9d489-158">Откройте файл **HelloWorldWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="9d489-158">Open the **HelloWorldWebPart.ts** file.</span></span>

<span data-ttu-id="9d489-159">Скопируйте следующий код и вставьте его под разделом `import * as strings from 'HelloWorldWebPartStrings';`.</span><span class="sxs-lookup"><span data-stu-id="9d489-159">Copy and paste the following code just below `import * as strings from 'HelloWorldWebPartStrings';`.</span></span>

```ts
import MockHttpClient from './MockHttpClient';
```
 
<span data-ttu-id="9d489-160">Добавьте приведенный ниже частный метод, имитирующий извлечение списков, в класс **HelloWorldWebPart**.</span><span class="sxs-lookup"><span data-stu-id="9d489-160">Add the following private method that mocks the list retrieval inside the **HelloWorldWebPart** class.</span></span>

```ts
  private _getMockListData(): Promise<ISPLists> {
    return MockHttpClient.get()
      .then((data: ISPList[]) => {
        var listData: ISPLists = { value: data };
        return listData;
      }) as Promise<ISPLists>;
  }
```

<span data-ttu-id="9d489-161">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="9d489-161">Save the file.</span></span>

## <a name="retrieve-lists-from-sharepoint-site"></a><span data-ttu-id="9d489-162">Получение списков с сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="9d489-162">Retrieve lists from SharePoint site</span></span>

<span data-ttu-id="9d489-p111">Далее нужно получить списки с текущего сайта. Чтобы получить списки с сайта https://yourtenantprefix.sharepoint.com/_api/web/lists, нужно использовать REST API SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d489-p111">Next you need to retrieve lists from the current site. You will use SharePoint REST APIs to retrieve the lists from the site, which are located at https://yourtenantprefix.sharepoint.com/_api/web/lists.</span></span>

<span data-ttu-id="9d489-165">Платформа SharePoint Framework включает вспомогательный класс **spHttpClient** для выполнения запросов REST API к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d489-165">SharePoint Framework includes a helper class **spHttpClient** to execute REST API requests against SharePoint.</span></span> <span data-ttu-id="9d489-166">Он добавляет заголовки, управляет дайджестом, необходимым для записи, и собирает данные телеметрии, которые помогают службе отслеживать производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="9d489-166">It adds default headers, manages the digest needed for writes, and collects telemetry that helps the service to monitor the performance of an application.</span></span>

<span data-ttu-id="9d489-167">Чтобы использовать этот вспомогательный класс, необходимо сначала импортировать его из модуля **@microsoft/sp-http**.</span><span class="sxs-lookup"><span data-stu-id="9d489-167">To use this helper class, you will first need to import them from the **@microsoft/sp-http** module.</span></span>

<span data-ttu-id="9d489-168">Прокрутите к началу файла **HelloWorldWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="9d489-168">Scroll to the top of the **HelloWorldWebPart.ts** file.</span></span> 

<span data-ttu-id="9d489-169">Скопируйте следующий код и вставьте его под разделом `import MockHttpClient from './MockHttpClient';`:</span><span class="sxs-lookup"><span data-stu-id="9d489-169">Copy and paste the following code just below `import MockHttpClient from './MockHttpClient';` :</span></span>

```ts
import {
  SPHttpClient,
  SPHttpClientResponse   
} from '@microsoft/sp-http';
```

<span data-ttu-id="9d489-170">Добавьте приведенный ниже частный метод для получения списков из SharePoint в класс **HelloWorldWebPart**.</span><span class="sxs-lookup"><span data-stu-id="9d489-170">Add the following private method to retrieve lists from SharePoint inside the **HelloWorldWebPart** class.</span></span>

```ts
private _getListData(): Promise<ISPLists> {
  return this.context.spHttpClient.get(this.context.pageContext.web.absoluteUrl + `/_api/web/lists?$filter=Hidden eq false`, SPHttpClient.configurations.v1)
    .then((response: SPHttpClientResponse) => {
      return response.json();
    });
}
```

<span data-ttu-id="9d489-171">Этот метод использует вспомогательный класс **spHttpClient** и отправляет запрос `get`.</span><span class="sxs-lookup"><span data-stu-id="9d489-171">The method uses the **spHttpClient** helper class and issues a `get` request.</span></span> <span data-ttu-id="9d489-172">Он использует модель **ISPLists**, а также применяет фильтр, чтобы не получать скрытые списки.</span><span class="sxs-lookup"><span data-stu-id="9d489-172">It uses the **ISPLists** model and also applies a filter to not retrieve hidden lists.</span></span>

<span data-ttu-id="9d489-173">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="9d489-173">Save the file.</span></span> 

<span data-ttu-id="9d489-p114">Перейдите в окно консоли, в котором запущена команда `gulp serve`, и проверьте наличие ошибок. Если gulp сообщил об ошибках, их нужно исправить.</span><span class="sxs-lookup"><span data-stu-id="9d489-p114">Switch to the console window that is running `gulp serve` and check if there are any errors. If there are errors, gulp reports them in the console and you will need to fix them before proceeding.</span></span>

## <a name="add-new-styles"></a><span data-ttu-id="9d489-176">Добавление новых стилей</span><span class="sxs-lookup"><span data-stu-id="9d489-176">Add new styles</span></span>

<span data-ttu-id="9d489-177">Платформа SharePoint Framework использует [Sass](http://sass-lang.com/) в качестве препроцессора CSS и, в частности, использует [синтаксис SCSS](http://sass-lang.com/documentation/file.SCSS_FOR_SASS_USERS.html), который полностью совместим со стандартным синтаксисом CSS.</span><span class="sxs-lookup"><span data-stu-id="9d489-177">The SharePoint Framework uses [Sass](http://sass-lang.com/) as the CSS pre-processor and specifically uses the [SCSS syntax](http://sass-lang.com/documentation/file.SCSS_FOR_SASS_USERS.html) which is fully complaint with normal CSS syntax.</span></span> <span data-ttu-id="9d489-178">Sass расширяет язык CSS и позволяет использовать такие функции, как переменные, вложенные правила и встроенные операции импорта, для упорядочения и создания эффективных таблиц стилей для веб-частей.</span><span class="sxs-lookup"><span data-stu-id="9d489-178">Sass extends the CSS language and allows you to use features like variables, nested rules, and inline imports to organize and create efficient style sheets for your web parts.</span></span> <span data-ttu-id="9d489-179">Платформа SharePoint Framework включает компилятор SCSS, который преобразует файлы Sass в обычные CSS-файлы, а также типизированную версию для использования во время разработки.</span><span class="sxs-lookup"><span data-stu-id="9d489-179">The SharePoint Framework already comes with a SCSS compiler that converts your Sass files to normal CSS files and also provides a typed version to use it in during development.</span></span>

<span data-ttu-id="9d489-180">Чтобы добавить новые стили, откройте файл **HelloWorld.module.scss**.</span><span class="sxs-lookup"><span data-stu-id="9d489-180">To add new styles, open **HelloWorld.module.scss**.</span></span> <span data-ttu-id="9d489-181">В этом SCSS-файле можно задавать стили.</span><span class="sxs-lookup"><span data-stu-id="9d489-181">This is the SCSS file where you will define your styles.</span></span>

<span data-ttu-id="9d489-182">По умолчанию стили действуют на уровне веб-части.</span><span class="sxs-lookup"><span data-stu-id="9d489-182">By default, the styles are scoped to your web part.</span></span> <span data-ttu-id="9d489-183">Это видно, так как стили задаются в разделе **.helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="9d489-183">You can see that as the styles are defined under **.helloWorld**.</span></span>

<span data-ttu-id="9d489-184">Добавьте следующие стили после стиля `.button` в главном разделе стилей `.helloWorld`:</span><span class="sxs-lookup"><span data-stu-id="9d489-184">Add the following styles after the `.button` style, but still inside of the main `.helloWorld` style section:</span></span>

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

<span data-ttu-id="9d489-185">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="9d489-185">Save the file.</span></span>

<span data-ttu-id="9d489-186">gulp перестраивает код в консоли, как только вы сохраняете файл.</span><span class="sxs-lookup"><span data-stu-id="9d489-186">gulp rebuilds the code in the console as soon as you save the file.</span></span> <span data-ttu-id="9d489-187">При этом создаются соответствующие определения типов в файле **HelloWorld.module.scss.ts**.</span><span class="sxs-lookup"><span data-stu-id="9d489-187">This will generate the corresponding typings in the **HelloWorld.module.scss.ts** file.</span></span> <span data-ttu-id="9d489-188">После компиляции для typescript вы можете импортировать эти стили и ссылаться на них в коде веб-части.</span><span class="sxs-lookup"><span data-stu-id="9d489-188">Once compiled to typescript, you can then import and reference these styles in your web part code.</span></span>

<span data-ttu-id="9d489-189">Это видно в методе **render** веб-части:</span><span class="sxs-lookup"><span data-stu-id="9d489-189">You can see that in the **render** method of the web part:</span></span>

```html
<div class="${styles.row}">
```

## <a name="method-to-render-lists-information"></a><span data-ttu-id="9d489-190">Метод отрисовки данных списков</span><span class="sxs-lookup"><span data-stu-id="9d489-190">Method to render lists information</span></span>

<span data-ttu-id="9d489-191">Перейдите к классу **HelloWorldWebPart**.</span><span class="sxs-lookup"><span data-stu-id="9d489-191">Open the **HelloWorldWebPart** class.</span></span>

<span data-ttu-id="9d489-192">SharePoint Workbench можно использовать для проверки веб-частей в локальной среде и на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d489-192">SharePoint Workbench gives you the flexibility to test web parts in your local environment and from a SharePoint site.</span></span> <span data-ttu-id="9d489-193">Платформа SharePoint Framework показывает, в какой среде запущена веб-часть, с помощью модуля **EnvironmentType**.</span><span class="sxs-lookup"><span data-stu-id="9d489-193">SharePoint Framework aids this capability by helping you understand which environment your web part is running from by using the **EnvironmentType** module.</span></span> 

<span data-ttu-id="9d489-194">Чтобы использовать модуль, сначала необходимо импортировать модули **Environment** и ***EnvironmentType** из пакета **@microsoft/sp-core-library**.</span><span class="sxs-lookup"><span data-stu-id="9d489-194">To use the module, you first need to import the **Environment** and the ***EnvironmentType** modules from the **@microsoft/sp-core-library** bundle.</span></span> <span data-ttu-id="9d489-195">Добавьте его в раздел **import** вверху, как показано в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="9d489-195">Add it to the **import** section at the top as shown in the following code:</span></span>

```ts
import {
  Environment,
  EnvironmentType
} from '@microsoft/sp-core-library';
```

<span data-ttu-id="9d489-196">Добавьте следующий частный метод в класс **HelloWorldWebPart** для вызова соответствующих методов и получения данных списков:</span><span class="sxs-lookup"><span data-stu-id="9d489-196">Add the following private method inside the **HelloWorldWebPart** class to call the respective methods to retrieve list data:</span></span>

```ts
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

<span data-ttu-id="9d489-197">Вот что нужно знать о hostType в методе **_renderListAsync**:</span><span class="sxs-lookup"><span data-stu-id="9d489-197">Things to note about hostType in the **_renderListAsync** method:</span></span>

* <span data-ttu-id="9d489-198">Свойство `Environment.type` поможет вам проверить, в какой среде вы находитесь (локальной или SharePoint).</span><span class="sxs-lookup"><span data-stu-id="9d489-198">The `Environment.type` property will help you check if you are in a local or SharePoint environment.</span></span>
* <span data-ttu-id="9d489-199">В зависимости от того, где размещается рабочая область, вызывается нужный метод.</span><span class="sxs-lookup"><span data-stu-id="9d489-199">The correct method is called depending on where your workbench is hosted.</span></span>

<span data-ttu-id="9d489-200">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="9d489-200">Save the file.</span></span>

<span data-ttu-id="9d489-201">Теперь данные списков нужно отрисовать при помощи значения, полученного из REST API.</span><span class="sxs-lookup"><span data-stu-id="9d489-201">Now you need to render the list data with the value fetched from the REST API.</span></span>

<span data-ttu-id="9d489-202">Добавьте следующий метод private в класс **HelloWorldWebPart**:</span><span class="sxs-lookup"><span data-stu-id="9d489-202">Add the following private method inside the **HelloWorldWebPart** class:</span></span>

```ts
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

<span data-ttu-id="9d489-203">Предыдущий метод ссылается на новые стили CSS, добавленные с помощью переменной **styles**.</span><span class="sxs-lookup"><span data-stu-id="9d489-203">The previous method references the new CSS styles added earlier by using the **styles** variable.</span></span> 

<span data-ttu-id="9d489-204">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="9d489-204">Save the file.</span></span>

## <a name="retrieve-list-data"></a><span data-ttu-id="9d489-205">Получение данных списков</span><span class="sxs-lookup"><span data-stu-id="9d489-205">Retrieve list data</span></span>

<span data-ttu-id="9d489-206">Замените код в методе **render** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="9d489-206">Navigate to the **render** method and replace the code inside the method with the following code:</span></span>

```ts
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

<span data-ttu-id="9d489-207">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="9d489-207">Save the file.</span></span>

<span data-ttu-id="9d489-208">В окне консоли вы заметите, что `gulp serve` перестраивает код.</span><span class="sxs-lookup"><span data-stu-id="9d489-208">Notice in the `gulp serve` console window that it rebuilds the code.</span></span> <span data-ttu-id="9d489-209">Убедитесь, что нет ошибок.</span><span class="sxs-lookup"><span data-stu-id="9d489-209">Make sure you don't see any errors.</span></span>

<span data-ttu-id="9d489-210">Перейдите в локальную рабочую область и добавьте веб-часть HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="9d489-210">Switch to your local workbench and add the HelloWorld web part.</span></span>

<span data-ttu-id="9d489-211">Должны появиться фиктивные данные.</span><span class="sxs-lookup"><span data-stu-id="9d489-211">You should see the mock data returned.</span></span>

![Отрисовка данных списков из localhost](../../../images/sp-lists-render-localhost.png)

<span data-ttu-id="9d489-p122">Перейдите в рабочую область, размещенную в SharePoint. Обновите страницу и добавьте веб-часть HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="9d489-p122">Switch to the workbench hosted in SharePoint. Refresh the page and add the HelloWorld web part.</span></span>

<span data-ttu-id="9d489-215">Должны появиться списки с текущего сайта.</span><span class="sxs-lookup"><span data-stu-id="9d489-215">You should see lists returned from the current site.</span></span>

![Отрисовка данных списков из SharePoint](../../../images/sp-lists-render-spsite.png)

<span data-ttu-id="9d489-217">Теперь вы можете остановить работу сервера.</span><span class="sxs-lookup"><span data-stu-id="9d489-217">Now you can stop the server from running.</span></span> <span data-ttu-id="9d489-218">Перейдите в консоль и остановите команду `gulp serve`.</span><span class="sxs-lookup"><span data-stu-id="9d489-218">Switch to the console and stop `gulp serve`.</span></span> <span data-ttu-id="9d489-219">Нажмите клавиши `Ctrl+C`, чтобы завершить задачу gulp.</span><span class="sxs-lookup"><span data-stu-id="9d489-219">Choose `Ctrl+C` to terminate the gulp task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d489-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9d489-220">Next steps</span></span>

<span data-ttu-id="9d489-221">Поздравляем: вы подключили веб-часть к данным списков SharePoint!</span><span class="sxs-lookup"><span data-stu-id="9d489-221">Congratulations on connecting your web part to SharePoint list data!</span></span> <span data-ttu-id="9d489-222">Из следующей статьи, которая называется [Развертывание веб-части на странице SharePoint](./serve-your-web-part-in-a-sharepoint-page.md),</span><span class="sxs-lookup"><span data-stu-id="9d489-222">You can continue building out your Hello World web part in the next topic [Deploy your web part to a SharePoint page](./serve-your-web-part-in-a-sharepoint-page.md).</span></span> <span data-ttu-id="9d489-223">вы узнаете, как развернуть и просмотреть веб-часть Hello World на странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d489-223">You will learn how to deploy and preview the Hello World web part in a classic SharePoint server-side page.</span></span>

> [!NOTE]
> <span data-ttu-id="9d489-224">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="9d489-224">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="9d489-225">Заранее спасибо!</span><span class="sxs-lookup"><span data-stu-id="9d489-225">Thanks for your input advance.</span></span>