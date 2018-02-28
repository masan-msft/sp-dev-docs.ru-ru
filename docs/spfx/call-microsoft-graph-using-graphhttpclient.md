---
title: "Вызов Microsoft Graph с помощью класса GraphHttpClient"
description: "Используйте класс GraphHttpClient для вызова REST API Microsoft Graph с помощью методов get(), post() и fetch()."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 898787fd3a9a2fa758b186a9ca9ae3627c579fa2
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="use-graphhttpclient-to-call-microsoft-graph"></a><span data-ttu-id="888c6-103">Вызов Microsoft Graph с помощью класса GraphHttpClient</span><span class="sxs-lookup"><span data-stu-id="888c6-103">Use GraphHttpClient to call Microsoft Graph</span></span>

> [!IMPORTANT]
> <span data-ttu-id="888c6-104">Класс **GraphHttpClient** находится на этапе тестирования, и в него могут быть внесены изменения.</span><span class="sxs-lookup"><span data-stu-id="888c6-104">The **GraphHttpClient** is currently in preview and is subject to change.</span></span> <span data-ttu-id="888c6-105">Сейчас он не поддерживается для использования в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="888c6-105">It is not currently supported for use in production environments.</span></span>

<span data-ttu-id="888c6-106">Используйте класс **GraphHttpClient** для вызова REST API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="888c6-106">Use the **GraphHttpClient** class to make calls to the Microsoft Graph REST API.</span></span> <span data-ttu-id="888c6-107">Вы можете выполнять запросы GET, POST и PATCH, используя методы **get()**, **post()** и **fetch()**.</span><span class="sxs-lookup"><span data-stu-id="888c6-107">You can make GET, POST, and PATCH requests using the **get()**, **post()**, and **fetch()** methods.</span></span> <span data-ttu-id="888c6-108">В этой статье рассказывается, как создать веб-часть на основе класса **GraphHttpClient**, но вы можете использовать класс **GraphHttpClient** в любом клиентском коде в SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="888c6-108">This article shows how to build a web part that uses **GraphHttpClient**, but you can use **GraphHttpClient** in any SharePoint Framework client code.</span></span>

## <a name="retrieve-office-365-groups-using-a-get-call"></a><span data-ttu-id="888c6-109">Получение групп Office 365 с помощью вызова GET</span><span class="sxs-lookup"><span data-stu-id="888c6-109">Retrieve Office 365 groups using a GET call</span></span>

<span data-ttu-id="888c6-110">Вы можете использовать метод **get()** для совершения вызова REST к Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="888c6-110">You can use the **get()** method to make a REST call to Microsoft Graph.</span></span> <span data-ttu-id="888c6-111">В этом примере показано, как получить список групп Office 365.</span><span class="sxs-lookup"><span data-stu-id="888c6-111">This example shows you how to retrieve a list of Office 365 groups.</span></span> 

### <a name="create-a-new-web-part-project"></a><span data-ttu-id="888c6-112">Создание проекта веб-части</span><span class="sxs-lookup"><span data-stu-id="888c6-112">Create a new web part project</span></span>

1. <span data-ttu-id="888c6-113">Создайте каталог проекта в любом расположении.</span><span class="sxs-lookup"><span data-stu-id="888c6-113">Create a new project directory in your favorite location.</span></span> 

  ```
  mkdir hellograph-webpart
  ```

2. <span data-ttu-id="888c6-114">Перейдите к каталогу проекта.</span><span class="sxs-lookup"><span data-stu-id="888c6-114">Go to the project directory.</span></span>

  ```
  cd hellograph-webpart
  ```

3. <span data-ttu-id="888c6-115">Создайте веб-часть, запустив генератор Yeoman для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="888c6-115">Create a new web part by running the Yeoman SharePoint generator.</span></span>

  ```
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="888c6-116">Когда отобразится соответствующий запрос, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="888c6-116">When prompted:</span></span>

  * <span data-ttu-id="888c6-117">Введите имя решения **hellograph-webpart**.</span><span class="sxs-lookup"><span data-stu-id="888c6-117">Enter a solution name of **hellograph-webpart**.</span></span>
  * <span data-ttu-id="888c6-118">В качестве расположения для размещения файлов выберите вариант **Использовать текущую папку**.</span><span class="sxs-lookup"><span data-stu-id="888c6-118">Select **Use the current folder** for where to place the files.</span></span>
  * <span data-ttu-id="888c6-119">Когда отобразится соответствующий запрос, введите **д**, если вы хотите разрешить администратору клиента развертывать решение немедленно на всех сайтах, не запуская процесс развертывания компонентов или добавления приложений на сайтах.</span><span class="sxs-lookup"><span data-stu-id="888c6-119">Enter **y** when prompted if you want to allow the tenant admin to deploy the solution to all sites immediately, without running any feature deployment or adding apps in sites.</span></span>
  * <span data-ttu-id="888c6-120">В качестве типа клиентского компонента, который необходимо создать, выберите вариант **Веб-часть**.</span><span class="sxs-lookup"><span data-stu-id="888c6-120">Select **Web Part** as the type of client-side component to create.</span></span>
  * <span data-ttu-id="888c6-121">В качестве имени веб-части введите **HelloGraph**.</span><span class="sxs-lookup"><span data-stu-id="888c6-121">Enter **HelloGraph** as your web part name.</span></span>
  * <span data-ttu-id="888c6-122">В качестве описания веб-части введите **Вызов API Групп Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="888c6-122">Enter **Calls the Microsoft Graph Groups API** as the web part description.</span></span>
  * <span data-ttu-id="888c6-123">Оставьте параметр **No javascript web framework** (Веб-платформа без JavaScript) без изменений и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="888c6-123">Accept the default **No javascript web framework** as the framework, and choose Enter.</span></span>

  ![Значения класса GraphHttpClient, которые необходимо ввести в командной строке](../images/graphhttpclient-web-part-create.jpg)

5. <span data-ttu-id="888c6-125">Генератор Yeoman создаст веб-часть.</span><span class="sxs-lookup"><span data-stu-id="888c6-125">The Yeoman generator will build the web part.</span></span> <span data-ttu-id="888c6-126">Когда шаблон будет сформирован, откройте папку проекта в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="888c6-126">When the scaffolding is finished, open your project folder in your code editor.</span></span> <span data-ttu-id="888c6-127">В этой статье в инструкциях и на снимках экрана используется Visual Studio Code, но вы можете использовать любой другой редактор.</span><span class="sxs-lookup"><span data-stu-id="888c6-127">This article uses Visual Studio Code in the steps and screenshots, but you can use any editor that you prefer.</span></span>

6. <span data-ttu-id="888c6-128">Выполните команду gulp serve и подтвердите, что она правильно выполняется на рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="888c6-128">Run the gulp serve command and confirm that it runs in the local workbench correctly.</span></span>

  ```
  gulp serve
  ```

### <a name="add-a-button-and-placeholder-for-results"></a><span data-ttu-id="888c6-129">Добавление кнопки и заполнителя для результатов</span><span class="sxs-lookup"><span data-stu-id="888c6-129">Add a button and placeholder for results</span></span>

<span data-ttu-id="888c6-130">Далее вы измените HTML-код и добавите кнопку для получения групп Office 365.</span><span class="sxs-lookup"><span data-stu-id="888c6-130">Next, you'll modify the HTML to provide a button to retrieve Office 365 groups.</span></span> <span data-ttu-id="888c6-131">В HTML-код также необходимо добавить заполнитель для отображения групп.</span><span class="sxs-lookup"><span data-stu-id="888c6-131">The HTML also needs a placeholder to display the groups.</span></span>

1. <span data-ttu-id="888c6-132">В редакторе кода откройте файл **/src/webparts/helloGraph/HelloGraphWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="888c6-132">In your code editor, open the **/src/webparts/helloGraph/HelloGraphWebPart.ts** file.</span></span>

2. <span data-ttu-id="888c6-133">Измените метод **render()** так, чтобы он содержал кнопку и раздел **div**, в котором код будет отображать группы Office 365 после их получения.</span><span class="sxs-lookup"><span data-stu-id="888c6-133">Modify the **render()** method so that it contains a button and a **div** where the code will list the Office 365 groups after they are retrieved.</span></span>

  <span data-ttu-id="888c6-134">Ваш код должен выглядеть, как указанный ниже TypeScript.</span><span class="sxs-lookup"><span data-stu-id="888c6-134">Your code should look like the following TypeScript.</span></span>

  ```typescript
    public render(): void {
      this.domElement.innerHTML = `
        <div class="${styles.helloGraph}">
        <div class="${styles.container}">
        <div class="ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}">
          <div class="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
            <span class="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
            <p class="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
            <p class="ms-font-l ms-fontColor-white">${escape(this.properties.description)}</p>
            <a href="https://aka.ms/spfx" class="${styles.button}">
              <span class="${styles.label}">Learn more</span>
            </a>
            <p>
            <input id="readGroups" type="button" value="Read Groups"/> 
            </p>
            <div id="spTableContainer" ></div>
          </div>
        </div>
      </div>
    </div>`;
    this.domElement.querySelector('#readGroups').addEventListener('click',() => {this._readGroups();});
    }
  ```

  <span data-ttu-id="888c6-135">Вы определите метод **_readGroups()** позже.</span><span class="sxs-lookup"><span data-stu-id="888c6-135">You'll define the **_readGroups()** method later.</span></span>

3. <span data-ttu-id="888c6-136">Определите интерфейс для представления каждой группы Office 365.</span><span class="sxs-lookup"><span data-stu-id="888c6-136">Define an interface to represent each Office 365 group.</span></span> <span data-ttu-id="888c6-137">Добавьте указанный ниже код непосредственно перед классом **HelloGraphWebPart**, но после операций импорта.</span><span class="sxs-lookup"><span data-stu-id="888c6-137">Add the following code just before the **HelloGraphWebPart** class but after the imports.</span></span>

  ```typescript
  export interface IOffice365Group {
    // Microsoft Graph has more group properties.
    displayName: string;
    mail: string;
    description: string;
  }
  ```

### <a name="use-the-graphhttpclientget-method-to-retrieve-office-365-groups"></a><span data-ttu-id="888c6-138">Получение групп Office 365 с помощью метода GraphHttpClient.get</span><span class="sxs-lookup"><span data-stu-id="888c6-138">Use the GraphHttpClient.get method to retrieve Office 365 groups</span></span>

<span data-ttu-id="888c6-139">Далее вы вызовете метод **GraphHttpClient.get()**, чтобы совершить вызов REST к Microsoft Graph и получить список групп Office 365.</span><span class="sxs-lookup"><span data-stu-id="888c6-139">Next, you'll call the **GraphHttpClient.get()** method to make a REST call to Microsoft Graph to retrieve a list of Office 365 groups.</span></span>

1. <span data-ttu-id="888c6-140">Импортируйте класс **GraphHttpClient** и связанные с ним типы, добавив указанный оператор импорта в начале файла **HelloGraphWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="888c6-140">Import the **GraphHttpClient** class and related types by adding the following import statement near the top of the **HelloGraphWebPart.ts** file.</span></span>

  ```typescript
  import { GraphHttpClient, HttpClientResponse, IGraphHttpClientOptions } from '@microsoft/sp-http';
  ```

2. <span data-ttu-id="888c6-141">Создайте метод **_readGroups()**, добавив указанный ниже код в класс **HelloGraphWebPart**.</span><span class="sxs-lookup"><span data-stu-id="888c6-141">Create the **_readGroups()** method by adding the following code to the **HelloGraphWebPart** class.</span></span>

  ```typescript
  protected _readGroups(){
      // Query for all groups on the tenant using Microsoft Graph.
      this.context.graphHttpClient.get(`v1.0/groups?$orderby=displayName`, GraphHttpClient.configurations.v1).then((response: HttpClientResponse) => {
        if (response.ok) {
          return response.json();
        } else {
          console.warn(response.statusText);
        }
      }).then((result: any) => {
        // Transfer result values to the group variable
        this._renderTable(result.value);
      });
  }
  ```

  <span data-ttu-id="888c6-142">В предыдущем фрагменте кода у свойства контекста имеется экземпляр класса GraphHttpClient.</span><span class="sxs-lookup"><span data-stu-id="888c6-142">In the previous code, the context property has the GraphHttpClient instance.</span></span> <span data-ttu-id="888c6-143">Когда вы вызываете метод **get()**, выполняется вызов REST к Microsoft Graph, который передает указанный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="888c6-143">When you call the **get()** method, a REST call is made to Microsoft Graph that passes the specified URL.</span></span> <span data-ttu-id="888c6-144">В данном случае используется следующий URL-адрес: **v1.0/groups?orderby=displayName**.</span><span class="sxs-lookup"><span data-stu-id="888c6-144">In this case, the URL is **v1.0/groups?orderby=displayName**.</span></span> <span data-ttu-id="888c6-145">В результате создается запрос GET, и Microsoft Graph возвращает все группы Office 365 в клиенте, отсортированные по отображаемому имени.</span><span class="sxs-lookup"><span data-stu-id="888c6-145">This issues a GET request and Microsoft Graph will return all Office 365 groups in the tenant in order by display name.</span></span>

  <span data-ttu-id="888c6-146">Вы можете создать любой запрос GET, использовав этот метод и введя правильные значения URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="888c6-146">You can issue any GET request by using this technique and entering the correct URL values.</span></span> <span data-ttu-id="888c6-147">Значения URL-адресов см. в [документации по Microsoft Graph](https://developer.microsoft.com/ru-RU/graph/docs/concepts/overview).</span><span class="sxs-lookup"><span data-stu-id="888c6-147">To find the URL values, see the [Microsoft Graph documentation](https://developer.microsoft.com/ru-RU/graph/docs/concepts/overview).</span></span> <span data-ttu-id="888c6-148">Например, для получения групп можно использовать URL-адрес, указанный в [этой статье](https://developer.microsoft.com/ru-RU/graph/docs/api-reference/v1.0/api/group_get).</span><span class="sxs-lookup"><span data-stu-id="888c6-148">For example, you can use URL specified in the [Groups GET request](https://developer.microsoft.com/ru-RU/graph/docs/api-reference/v1.0/api/group_get) topic to get groups.</span></span> 

  <span data-ttu-id="888c6-149">Метод **get()** возвращает объект **HttpClientResponse**, который позволяет определить, успешно ли выполнен вызов.</span><span class="sxs-lookup"><span data-stu-id="888c6-149">The **get()** method returns an **HttpClientResponse**, which you can use to determine whether the call was successful.</span></span> <span data-ttu-id="888c6-150">Возвращенный объект JSON находится в объекте **result.value**.</span><span class="sxs-lookup"><span data-stu-id="888c6-150">The returned JSON is in the **result.value**.</span></span> <span data-ttu-id="888c6-151">Так как вы ожидаете получить несколько групп, вы передаете значение в метод **_renderTable()**, который создает таблицу строк для каждой группы.</span><span class="sxs-lookup"><span data-stu-id="888c6-151">Because you expect multiple groups to be returned, you will pass the value to a **_renderTable()** method, which will build a table of rows for each group.</span></span>

3. <span data-ttu-id="888c6-152">Создайте метод **_renderTable()** для отображения возвращенных групп в таблице, в которой каждая строка представляет отдельную группу.</span><span class="sxs-lookup"><span data-stu-id="888c6-152">Create a **_renderTable()** method to render the returned groups in a table where each row represent a group.</span></span> <span data-ttu-id="888c6-153">Добавьте указанный ниже метод в класс **HelloGraphWebPart**.</span><span class="sxs-lookup"><span data-stu-id="888c6-153">Add the following method to the **HelloGraphWebPart** class.</span></span>

  ```typescript
  protected _renderTable(items: IOffice365Group[]): void {
    let html: string = '';
    if (items.length<=0){
      html=`<p>There are no groups to list...</p>`;
    }
    else {
      html += `
      <table><tr>
        <th>Display Name</th>
        <th>Mail</th>
        <th>Description</th></tr>`;
      items.forEach((item: IOffice365Group) => {
        html += `
          <tr>
              <td>${item.displayName}</td>
              <td>${item.mail}</td>
              <td>${item.description}</td>
          </tr>`;
      });
      html += `</table>`;
    }
    const tableContainer: Element = this.domElement.querySelector('#spTableContainer');
    tableContainer.innerHTML = html;
    return;
  }
  ```

### <a name="run-the-web-part-to-call-microsoft-graph"></a><span data-ttu-id="888c6-154">Запуск веб-части для вызова Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="888c6-154">Run the web part to call Microsoft Graph</span></span>

<span data-ttu-id="888c6-155">Коду необходимо вызвать приложение **GraphHttpClient**, которое выполняется в SharePoint, поэтому вам не удастся запустить его на локальном рабочем месте.</span><span class="sxs-lookup"><span data-stu-id="888c6-155">The code needs to call the **GraphHttpClient** application that runs on SharePoint, so you can't run it on the local workbench.</span></span> <span data-ttu-id="888c6-156">Вам придется упаковать и развернуть его в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="888c6-156">You have to package and deploy it to SharePoint.</span></span>

1. <span data-ttu-id="888c6-157">Упакуйте решение с помощью команды gulp.</span><span class="sxs-lookup"><span data-stu-id="888c6-157">Use gulp to package your solution.</span></span>

  ```
  gulp package-solution
  ```

2. <span data-ttu-id="888c6-158">Разверните решение в своем клиенте SharePoint, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="888c6-158">Deploy the solution to your SharePoint tenant:</span></span>
  * <span data-ttu-id="888c6-159">Перейдите в каталог приложений вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="888c6-159">Go to your site's App Catalog.</span></span>
  * <span data-ttu-id="888c6-160">Отправьте или перетащите файл **hellograph-webpart.sppkg** в каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="888c6-160">Upload or drag and drop the **hellograph-webpart.sppkg** to the App Catalog.</span></span>
  * <span data-ttu-id="888c6-161">Если вы доверяете **hellograph-webpart-client-side-solution**, выберите **Сделать это решение доступным для всех сайтов в организации** и нажмите кнопку **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="888c6-161">When prompted, if you trust the **hellograph-webpart-client-side-solution**, select **Make this solution available to all sites in the organization**, and choose **Deploy**.</span></span>

3. <span data-ttu-id="888c6-162">Разместите веб-часть с помощью команды gulp serve.</span><span class="sxs-lookup"><span data-stu-id="888c6-162">Use gulp serve to host the web part.</span></span>

  ```
  gulp serve --nobrowser
  ```

4. <span data-ttu-id="888c6-163">Добавьте веб-часть на веб-страницу или используйте SharePoint Workbench.</span><span class="sxs-lookup"><span data-stu-id="888c6-163">Add the web part to a web page, or use the SharePoint workbench.</span></span>

  <span data-ttu-id="888c6-164">Страница должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="888c6-164">You should see the following on your page.</span></span>

  ![Веб-часть GraphHttpClient с кнопкой чтения групп и одной группой в таблице](../images/graphhttpclient-read-groups-display.jpg)

  <span data-ttu-id="888c6-166">Если вы нажмете кнопку **Read Groups** (Прочитать группы), отобразится список всех групп Office 365 в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="888c6-166">When you choose **Read Groups**, you will see a list of all the Office 365 groups on your tenant.</span></span> <span data-ttu-id="888c6-167">Если в списке нет ни одной группы, отобразится сообщение, в котором будет указано, что нет ни одной группы.</span><span class="sxs-lookup"><span data-stu-id="888c6-167">If no groups are listed, you'll just see a message that indicates that there were no groups.</span></span> <span data-ttu-id="888c6-168">Далее вы создадите группу.</span><span class="sxs-lookup"><span data-stu-id="888c6-168">You will create a new group next.</span></span>

## <a name="create-a-new-office-365-group-using-a-post-call"></a><span data-ttu-id="888c6-169">Создание группы Office 365 с помощью вызова POST</span><span class="sxs-lookup"><span data-stu-id="888c6-169">Create a new Office 365 group using a POST call</span></span>

<span data-ttu-id="888c6-170">Вы можете совершать вызовы POST к API Microsoft Graph, используя метод **GraphHttpClient.post()**.</span><span class="sxs-lookup"><span data-stu-id="888c6-170">You can issue POST calls to the Microsoft Graph API by using the **GraphHttpClient.post()** method.</span></span> <span data-ttu-id="888c6-171">Вы создадите группу Office 365, используя метод **post()**.</span><span class="sxs-lookup"><span data-stu-id="888c6-171">You'll use the **post()** method to create a new Office 365 group.</span></span>


### <a name="add-a-button-and-placeholder-for-results"></a><span data-ttu-id="888c6-172">Добавление кнопки и заполнителя для результатов</span><span class="sxs-lookup"><span data-stu-id="888c6-172">Add a button and placeholder for results</span></span>

<span data-ttu-id="888c6-173">Чтобы добавить кнопку для создания группы, изменить HTML-код.</span><span class="sxs-lookup"><span data-stu-id="888c6-173">Again, you need to modify the HTML to add a button that will create a new group.</span></span>

1. <span data-ttu-id="888c6-174">В редакторе кода откройте файл **/src/webparts/helloGraph/HelloGraphWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="888c6-174">In your code editor, open the **/src/webparts/helloGraph/HelloGraphWebPart.ts** file.</span></span>

2. <span data-ttu-id="888c6-175">Измените метод **render()** так, чтобы он содержал кнопку и раздел **div**, который будет сигнализировать об успешности создания группы.</span><span class="sxs-lookup"><span data-stu-id="888c6-175">Modify the **render()** method so that it contains a button and a **div** that will indicate whether the creation was successful.</span></span>

  <span data-ttu-id="888c6-176">Ваш код должен выглядеть, как указанный ниже TypeScript.</span><span class="sxs-lookup"><span data-stu-id="888c6-176">Your code should look like the following TypeScript.</span></span>

  ```typescript
    public render(): void {
      this.domElement.innerHTML = `
        <div class="${styles.helloGraph}">
        <div class="${styles.container}">
        <div class="ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}">
          <div class="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
            <span class="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
            <p class="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
            <p class="ms-font-l ms-fontColor-white">${escape(this.properties.description)}</p>
            <a href="https://aka.ms/spfx" class="${styles.button}">
              <span class="${styles.label}">Learn more</span>
            </a>
            <p>
            <input id="readGroups" type="button" value="Read Groups"/> 
            <input id="createGroup" type="button" value="Create New Group"/>                           
            </p>
            <div id="spCreateGroupResults" ></div>
            <div id="spTableContainer" ></div>
          </div>
        </div>
      </div>
    </div>`;
    this.domElement.querySelector('#createGroup').addEventListener('click',() => {this._createGroup();});
    this.domElement.querySelector('#readGroups').addEventListener('click',() => {this._readGroups();});    
    }
  ```

3. <span data-ttu-id="888c6-177">Добавьте метод **_createGroup()** для вызова API Microsoft Graph и создания группы.</span><span class="sxs-lookup"><span data-stu-id="888c6-177">Add the **_createGroup()** method to call the Microsoft Graph API and create a new group.</span></span>

  ```typescript
    protected _createGroup(){
      // Use Microsoft Graph to create a sample group.
      this.context.graphHttpClient.post(`v1.0/groups`,GraphHttpClient.configurations.v1,{
        body: JSON.stringify({"description": "Self help community for library",
        "displayName": "Library Assist",
        "groupTypes": [
          "Unified"
        ],
        "mailEnabled": true,
        "mailNickname": "library",
        "securityEnabled": false
      })
    }).then((response: HttpClientResponse) => {
      const resultContainer: Element = this.domElement.querySelector('#spCreateGroupResults');
        if (response.ok) {
          resultContainer.innerHTML = `<p>Sample group created</p>`;
        } else {
          resultContainer.innerHTML = `<p>Could not create group see console for details</p>`;        
          console.warn(response.status);
        }
      });
    }
  ```

  <span data-ttu-id="888c6-178">Показанный выше код создает простую группу, используя пример кода из статьи [Создание группы](https://developer.microsoft.com/ru-RU/graph/docs/api-reference/v1.0/api/group_post_groups), посвященной Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="888c6-178">The previous code creates a simple group using the code example from the Microsoft Graph [Create group](https://developer.microsoft.com/ru-RU/graph/docs/api-reference/v1.0/api/group_post_groups) article.</span></span>

  <span data-ttu-id="888c6-179">Метод **post()** совершает вызов REST API POST по URL-адресу **v1.0/groups**.</span><span class="sxs-lookup"><span data-stu-id="888c6-179">The **post()** issues a POST REST API call to the **v1.0/groups** URL.</span></span> <span data-ttu-id="888c6-180">Третий параметр — значение **IGraphHttpClientOptions**, в котором указано тело JSON для описания новой группы.</span><span class="sxs-lookup"><span data-stu-id="888c6-180">The third parameter is an **IGraphHttpClientOptions** value in which the JSON body is specified to describe the new group.</span></span> <span data-ttu-id="888c6-181">Класс **HttpClientResponse** используется для определения успешности выполнения вызова и для отображения соответствующего результата.</span><span class="sxs-lookup"><span data-stu-id="888c6-181">The **HttpClientResponse** is used to determine whether the call was successful, and to display an appropriate result.</span></span>

  <span data-ttu-id="888c6-182">Вы можете совершить вызов POST из документации по Microsoft Graph, использовав этот шаблон и указав объект JSON в теле.</span><span class="sxs-lookup"><span data-stu-id="888c6-182">You can issue a POST call from the Microsoft Graph documentation by using this pattern and specifying the JSON in the body.</span></span>

### <a name="run-the-web-part-to-create-a-new-group"></a><span data-ttu-id="888c6-183">Запуск веб-части для создания группы</span><span class="sxs-lookup"><span data-stu-id="888c6-183">Run the web part to create a new group</span></span>

1. <span data-ttu-id="888c6-184">Упакуйте решение с помощью команды gulp.</span><span class="sxs-lookup"><span data-stu-id="888c6-184">Use gulp to package your solution.</span></span>

  ```
  gulp package-solution
  ```

2. <span data-ttu-id="888c6-185">Разверните решение в своем клиенте SharePoint, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="888c6-185">Deploy the solution to your SharePoint tenant:</span></span>
  * <span data-ttu-id="888c6-186">Перейдите в каталог приложений вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="888c6-186">Go to your site's App Catalog.</span></span>
  * <span data-ttu-id="888c6-187">Отправьте или перетащите файл **hellograph-webpart.sppkg** в каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="888c6-187">Upload or drag and drop the **hellograph-webpart.sppkg** to the App Catalog.</span></span>
  * <span data-ttu-id="888c6-188">Так как ваше решение уже зарегистрировано, система спросит, следует ли его заменить.</span><span class="sxs-lookup"><span data-stu-id="888c6-188">Because your solution is already registered, you'll be prompted as to whether you want to replace it.</span></span> <span data-ttu-id="888c6-189">Нажмите **Заменить**.</span><span class="sxs-lookup"><span data-stu-id="888c6-189">Select **Replace It**.</span></span>
  * <span data-ttu-id="888c6-190">Когда система спросит, доверяете ли вы решению, выберите **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="888c6-190">When prompted as to whether you trust the solution, choose **Deploy**.</span></span>

3. <span data-ttu-id="888c6-191">Разместите веб-часть с помощью команды gulp serve.</span><span class="sxs-lookup"><span data-stu-id="888c6-191">Use gulp serve to host the web part.</span></span>

  ```
  gulp serve --nobrowser
  ```

4. <span data-ttu-id="888c6-192">Добавьте веб-часть на веб-страницу или используйте SharePoint Workbench.</span><span class="sxs-lookup"><span data-stu-id="888c6-192">Add the web part to a web page, or use the SharePoint workbench.</span></span>

  <span data-ttu-id="888c6-193">Страница должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="888c6-193">You should see the following on your page.</span></span>

  ![Веб-часть GraphHttpClient с кнопкой создания группы и сообщением о том, что группа успешно создана](../images/graphhttpclient-group-created.jpg)

5. <span data-ttu-id="888c6-195">При нажатии кнопки **Create New Group** код создает группу Office 365.</span><span class="sxs-lookup"><span data-stu-id="888c6-195">When you choose **Create New Group**, the code will create a new Office 365 group.</span></span> 

  > [!NOTE] 
  > <span data-ttu-id="888c6-196">При повторной попытке создать ту же группу код возвращает ошибку, так как группа уже существует.</span><span class="sxs-lookup"><span data-stu-id="888c6-196">If you try to create the same group again, the code will return an error because the group already exists.</span></span> <span data-ttu-id="888c6-197">Ошибка записывается в консоли, которую можно просмотреть в режиме разработчика в браузере.</span><span class="sxs-lookup"><span data-stu-id="888c6-197">The error is logged to the console, which you can view in the browser's developer mode.</span></span>

## <a name="update-a-group-using-a-patch-call"></a><span data-ttu-id="888c6-198">Изменение группы с помощью вызова PATCH</span><span class="sxs-lookup"><span data-stu-id="888c6-198">Update a group using a PATCH call</span></span>

<span data-ttu-id="888c6-199">К данному моменту вы должны были разобраться в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="888c6-199">By now you should understand the pattern.</span></span> <span data-ttu-id="888c6-200">Если вам необходимо совершить вызов к REST API Microsoft Graph, используйте для запроса метод **get()** или **post()** с URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="888c6-200">If you need to call a Microsoft Graph REST API, use the **get()** or **post()** methods along with the URL for your request.</span></span> <span data-ttu-id="888c6-201">Последний метод, о котором следует рассказать, — метод **fetch()**.</span><span class="sxs-lookup"><span data-stu-id="888c6-201">The last method to show is the **fetch()** method.</span></span> <span data-ttu-id="888c6-202">С помощью этого метода вы можете создать запрос PATCH к Microsoft Graph для изменения ресурса.</span><span class="sxs-lookup"><span data-stu-id="888c6-202">This method allows you to issue a PATCH request to Microsoft Graph to update a resource.</span></span>

<span data-ttu-id="888c6-203">В коде ниже показано, как вызвать метод **fetch()** для изменения существующей группы.</span><span class="sxs-lookup"><span data-stu-id="888c6-203">The following code shows how to call the **fetch()** method to update an existing group.</span></span>

```typescript
    this.context.graphHttpClient.fetch(`v1.0/groups/2dfead70-21e4-4f30-bb2b-94b1bbdefdfa`,GraphHttpClient.configurations.v1,{
      method: "PATCH",
      body: JSON.stringify(
        {
          "description": "This is the new description",
          "displayName": "testtest"
        })
  }).then((response: HttpClientResponse) => {
    const resultContainer: Element = this.domElement.querySelector('#spUpdateGroupResults');
      if (response.ok) {
        resultContainer.innerHTML = `<p>Group updated</p>`;
      } else {
        resultContainer.innerHTML = `<p>Could not update group see console for details</p>`;        
        console.warn(response.status);
      }
    });
```

<span data-ttu-id="888c6-204">Идентификатор группы указан в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="888c6-204">The ID of the group is specified in the URL.</span></span> <span data-ttu-id="888c6-205">Получите идентификатор, выполнив сначала вызов GET.</span><span class="sxs-lookup"><span data-stu-id="888c6-205">Get the ID by using a GET call first.</span></span> <span data-ttu-id="888c6-206">Параметр **method** имеет значение **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="888c6-206">The **method** parameter is set to **PATCH**.</span></span> <span data-ttu-id="888c6-207">В теле указано, свойства какой группы необходимо изменить.</span><span class="sxs-lookup"><span data-stu-id="888c6-207">The body specifies which group properties to modify.</span></span>

## <a name="see-also"></a><span data-ttu-id="888c6-208">См. также</span><span class="sxs-lookup"><span data-stu-id="888c6-208">See also</span></span>

- [<span data-ttu-id="888c6-209">Обзор класса GraphHttpClient</span><span class="sxs-lookup"><span data-stu-id="888c6-209">Overview of the GraphHttpClient class (preview)</span></span>](overview-graphhttpclient.md)
