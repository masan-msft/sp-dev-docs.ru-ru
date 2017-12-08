---
title: "Перенос приложений AngularJS на платформу SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: cd07f02873ed476e298dcbbc17014cbc2443639b
ms.sourcegitcommit: 9c458121628425716442abddbc97a1f61f18a74c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2017
---
# <a name="migrate-angularjs-applications-to-sharepoint-framework"></a><span data-ttu-id="91c69-102">Перенос приложений AngularJS на платформу SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="91c69-102">Migrate Angular v1.x applications to SharePoint Framework</span></span>

<span data-ttu-id="91c69-103">Раньше во многих организациях решения для SharePoint создавались с помощью AngularJS.</span><span class="sxs-lookup"><span data-stu-id="91c69-103">Many organizations have been using AngularJS for building SharePoint solutions in the past.</span></span> <span data-ttu-id="91c69-104">В этой статье показано, как перенести имеющееся приложение AngularJS, стиль которого создан с помощью [ngOfficeUIFabric](http://ngofficeuifabric.com) (директив AngularJS для Office UI Fabric), в клиентскую веб-часть SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="91c69-104">This article shows how to migrate an existing AngularJS application styled using [ngOfficeUIFabric](http://ngofficeuifabric.com) - AngularJS directives for Office UI Fabric, to a SharePoint Framework client-side web part.</span></span> <span data-ttu-id="91c69-105">Приложение, используемое в этом руководстве, управляет элементами списка дел, сохраненными в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="91c69-105">The sample application used for this tutorial manages to do items stored in a SharePoint list.</span></span>

![Приложение AngularJS для управления элементами списка дел, сохраненными в списке SharePoint](../../../images/ng-migration-original-angular-application.png)

<span data-ttu-id="91c69-107">Исходный код приложения AngularJS доступен на сайте GitHub по адресу [https://github.com/SharePoint/sp-dev-fx-webparts/tree/dev/samples/angular-migration/angular-todo](https://github.com/SharePoint/sp-dev-fx-webparts/tree/dev/samples/angular-migration/angular-todo).</span><span class="sxs-lookup"><span data-stu-id="91c69-107">The source of the Angular application is available on GitHub at [https://github.com/SharePoint/sp-dev-fx-webparts/tree/dev/samples/angular-migration/angular-todo](https://github.com/SharePoint/sp-dev-fx-webparts/tree/dev/samples/angular-migration/angular-todo).</span></span>

<span data-ttu-id="91c69-108">Исходный код приложения AngularJS, перенесенного на платформу SharePoint Framework, доступен на сайте GitHub по адресу [https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/angular-todo](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/angular-todo).</span><span class="sxs-lookup"><span data-stu-id="91c69-108">The source of the Angular application migrated to SharePoint Framework is available on GitHub at [https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/angular-todo-webpart](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/angular-todo).</span></span>

> <span data-ttu-id="91c69-109">**Примечание.** Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки](http://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment) для создания решений на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="91c69-109">**Note:** Before following the steps in this article, be sure to [set up your development environment](http://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment) for building SharePoint Framework solutions.</span></span>

## <a name="setup-project"></a><span data-ttu-id="91c69-110">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="91c69-110">Setup project</span></span>

<span data-ttu-id="91c69-111">Прежде чем приступить к переносу приложения AngularJS, создайте и настройте новый проект на платформе SharePoint Framework для размещения приложения AngularJS.</span><span class="sxs-lookup"><span data-stu-id="91c69-111">Before you start migrating your Angular application, create and setup new SharePoint Framework project to host the Angular application.</span></span>

### <a name="create-new-project"></a><span data-ttu-id="91c69-112">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="91c69-112">Create new project</span></span>

<span data-ttu-id="91c69-113">Для начала создайте папку проекта.</span><span class="sxs-lookup"><span data-stu-id="91c69-113">Start by creating a new folder for your project</span></span>

```sh
md angular-todo
```

<span data-ttu-id="91c69-114">Перейдите в папку проекта:</span><span class="sxs-lookup"><span data-stu-id="91c69-114">Navigate to the project folder:</span></span>

```sh
cd angular-todo
```

<span data-ttu-id="91c69-115">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework:</span><span class="sxs-lookup"><span data-stu-id="91c69-115">In the project folder run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project:</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="91c69-116">Определите значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="91c69-116">When prompted, define values as follows:</span></span>

- <span data-ttu-id="91c69-117">**angular-todo** как имя решения</span><span class="sxs-lookup"><span data-stu-id="91c69-117">**angular-todo** as your solution name</span></span>
- <span data-ttu-id="91c69-118">расположение файлов — **Use the current folder** (Использовать текущую папку)</span><span class="sxs-lookup"><span data-stu-id="91c69-118">**Use the current folder** for the location to place the files</span></span>
- <span data-ttu-id="91c69-119">имя веб-части — **To do** (Текущие дела)</span><span class="sxs-lookup"><span data-stu-id="91c69-119">**To do** as your web part name</span></span>
- <span data-ttu-id="91c69-120">описание веб-части — **Simple management of to do tasks** (Простое управление задачами)</span><span class="sxs-lookup"><span data-stu-id="91c69-120">**Simple management of to do tasks** as your web part description</span></span>
- <span data-ttu-id="91c69-121">отправная точка создания веб-части — **No JavaScript web framework** (Без веб-платформы JavaScript).</span><span class="sxs-lookup"><span data-stu-id="91c69-121">**No JavaScript web framework** as the starting point to build the web part</span></span>

![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/ng-migration-yeoman-generator.png)

<span data-ttu-id="91c69-123">После завершения скаффолдинга блокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="91c69-123">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

```sh
npm shrinkwrap
```

<span data-ttu-id="91c69-124">Далее откройте папку проекта в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="91c69-124">Next, open your project folder in your code editor.</span></span> <span data-ttu-id="91c69-125">В этом руководстве используется Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="91c69-125">Once the scaffolding completes, open your project folder in your code editor. In this tutorial, you will use Visual Studio Code.</span></span>

![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/ng-migration-project-visual-studio-code.png)

### <a name="add-angularjs-and-ngofficeuifabric"></a><span data-ttu-id="91c69-127">Добавление AngularJS и ngOfficeUIFabric</span><span class="sxs-lookup"><span data-stu-id="91c69-127">Add Angular and ngOfficeUIFabric</span></span>

<span data-ttu-id="91c69-128">В этом руководстве AngularJS и ngOfficeUIFabric загружаются из CDN.</span><span class="sxs-lookup"><span data-stu-id="91c69-128">In this tutorial you will load both AngularJS and ngOfficeUIFabric from CDN.</span></span> <span data-ttu-id="91c69-129">Для этого откройте в редакторе кода файл **config/config.json** и добавьте следующие строки в свойстве **externals**:</span><span class="sxs-lookup"><span data-stu-id="91c69-129">In this tutorial you will load Angular from CDN. To do that, in the code editor, open the **config/config.json** file and in the **externals** property add the following lines:</span></span>

```json
"angular": {
  "path": "https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.6.6/angular.min.js",
  "globalName": "angular"
},
"ng-office-ui-fabric": "https://cdnjs.cloudflare.com/ajax/libs/ngOfficeUiFabric/0.12.3/ngOfficeUiFabric.js"
```

### <a name="add-angularjs-typings-for-typescript"></a><span data-ttu-id="91c69-130">Добавление определений типа AngularJS для TypeScript</span><span class="sxs-lookup"><span data-stu-id="91c69-130">Add Angular typings for TypeScript</span></span>

<span data-ttu-id="91c69-131">Так как в коде веб-части вы будете ссылаться на AngularJS, вам также потребуются определения типов AngularJS для TypeScript.</span><span class="sxs-lookup"><span data-stu-id="91c69-131">Because you will be referencing Angular in your web part's code, you also need Angular typings for TypeScript. To install them run in the command line:</span></span> <span data-ttu-id="91c69-132">Чтобы установить их, выполните в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="91c69-132">To install them run in the command line:</span></span>

```sh
npm install @types/angular --save-dev
```

## <a name="migrate-the-angularjs-application-as-is"></a><span data-ttu-id="91c69-133">Перенос приложения AngularJS "как есть"</span><span class="sxs-lookup"><span data-stu-id="91c69-133">Migrate the Angular application as-is</span></span>

<span data-ttu-id="91c69-134">Для начала мы перенесем приложение AngularJS с минимальными изменениями кода.</span><span class="sxs-lookup"><span data-stu-id="91c69-134">Start with migrating the AngularJS application with only the minimal code changes.</span></span> <span data-ttu-id="91c69-135">Позже мы обновим обычный код JavaScript приложения до TypeScript и улучшим его интеграцию с клиентской веб-частью.</span><span class="sxs-lookup"><span data-stu-id="91c69-135">Start with migrating the Angular application with only the minimal code changes. Later, you will upgrade the application's plain JavaScript code to TypeScript and improve its integration with the client-side web part.</span></span>

### <a name="create-sharepoint-list"></a><span data-ttu-id="91c69-136">Создание списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="91c69-136">Create SharePoint list</span></span>

<span data-ttu-id="91c69-137">Создайте на сайте SharePoint новый список под названием **Todo** (Список дел).</span><span class="sxs-lookup"><span data-stu-id="91c69-137">In your SharePoint site create a new list called Todo. In the list add a new choice column called Status. As available choices enter:</span></span> <span data-ttu-id="91c69-138">Добавьте в список новый столбец вариантов под названием **Status** (Состояние).</span><span class="sxs-lookup"><span data-stu-id="91c69-138">In your SharePoint site create a new list called Todo. In the list add a new choice column called Status. As available choices enter:</span></span> <span data-ttu-id="91c69-139">Укажите следующие варианты:</span><span class="sxs-lookup"><span data-stu-id="91c69-139">As available choices enter:</span></span>

```text
Not started
In progress
Completed
```

![Список дел в SharePoint](../../../images/ng-migration-todo-list.png)

### <a name="copy-angularjs-application-files-to-the-web-part-project"></a><span data-ttu-id="91c69-141">Копирование файлов приложения AngularJS в проект веб-части</span><span class="sxs-lookup"><span data-stu-id="91c69-141">Copy Angular application files to the web part project</span></span>

<span data-ttu-id="91c69-142">В проекте веб-части создайте в папке **src/webparts/toDo** дочернюю папку с именем `app`.</span><span class="sxs-lookup"><span data-stu-id="91c69-142">In the web part project, in the **src/webparts/toDo** folder create a new folder called `app`.</span></span>

![Папка приложения, выделенная в области обозревателя Visual Studio Code](../../../images/ng-migration-app-folder-visual-studio-code.png)

<span data-ttu-id="91c69-144">Скопируйте содержимое папки **app** из исходного приложения в новую папку **app** проекта веб-части.</span><span class="sxs-lookup"><span data-stu-id="91c69-144">From the source application copy the contents of the **app** folder, to the newly created **app** folder in the web part project.</span></span>

![Файлы приложения, выделенные в области обозревателя Visual Studio Code](../../../images/ng-migration-app-files-visual-studio-code.png)

### <a name="load-the-angularjs-application-in-the-client-side-web-part"></a><span data-ttu-id="91c69-146">Загрузка приложения AngularJS в клиентской веб-части</span><span class="sxs-lookup"><span data-stu-id="91c69-146">Load the Angular application in the client-side web part</span></span>

<span data-ttu-id="91c69-147">В редакторе кода откройте файл **./src/webparts/toDo/ToDoWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="91c69-147">In the code editor open the **./src/webparts/toDo/ToDoWebPart.ts** file.</span></span>

<span data-ttu-id="91c69-148">После последнего оператора `import` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="91c69-148">After the last `import` statement add the following code:</span></span>

```ts
import * as angular from 'angular';
import 'ng-office-ui-fabric';
```

<span data-ttu-id="91c69-149">Замените содержимое метода **render** на следующий код:</span><span class="sxs-lookup"><span data-stu-id="91c69-149">Change the contents of the **render** method to:</span></span>

```ts
export default class ToDoWebPart extends BaseClientSideWebPart<IToDoWebPartProps> {
  // ...
  public render(): void {
    if (this.renderedOnce === false) {
      require('./app/app.module');
      require('./app/app.config');
      require('./app/data.service');
      require('./app/home.controller');

      this.domElement.innerHTML = `
        <div class="${styles.toDo}">
          <div data-ng-controller="homeController as vm">
            <div class="${styles.loading}" ng-show="vm.isLoading">
              <uif-spinner>Loading...</uif-spinner>
            </div>
            <div class="entryform" ng-show="vm.isLoading === false">
              <uif-textfield uif-label="New to do:" uif-underlined ng-model="vm.newItem" ng-keydown="vm.todoKeyDown($event)"></uif-textfield>
            </div>
            <uif-list class="items" ng-show="vm.isLoading === false" >
              <uif-list-item ng-repeat="todo in vm.todoCollection" uif-item="todo" ng-class="{'done': todo.done}">
                <uif-list-item-primary-text>{{todo.title}}</uif-list-item-primary-text>
                <uif-list-item-actions>
                  <uif-list-item-action ng-click="vm.completeTodo(todo)" ng-show="todo.done === false">
                    <uif-icon uif-type="check"></uif-icon>
                  </uif-list-item-action>
                  <uif-list-item-action ng-click="vm.undoTodo(todo)" ng-show="todo.done">
                    <uif-icon uif-type="reactivate"></uif-icon>
                  </uif-list-item-action>
                  <uif-list-item-action ng-click="vm.deleteTodo(todo)">
                    <uif-icon uif-type="trash"></uif-icon>
                  </uif-list-item-action>
                </uif-list-item-actions>
              </uif-list-item>
            </uif-list>
          </div>
        </div>`;

      angular.bootstrap(this.domElement, ['todoapp']);
    }
  }
  // ...
}
```

### <a name="update-site-path"></a><span data-ttu-id="91c69-150">Обновление пути к сайту</span><span class="sxs-lookup"><span data-stu-id="91c69-150">Update site path</span></span>

<span data-ttu-id="91c69-151">Откройте в редакторе кода файл **./src/webparts/toDo/app/app.config.js**.</span><span class="sxs-lookup"><span data-stu-id="91c69-151">In the code editor open the **./src/webparts/toDo/app/app.config.js** file.</span></span> <span data-ttu-id="91c69-152">Замените значение константы **sharepointApi** на относительный касательно сервера URL-адрес для сайта SharePoint, на котором создан список дел, и добавьте к нему строку `/_api/`.</span><span class="sxs-lookup"><span data-stu-id="91c69-152">In the code editor open the ./src/webparts/toDo/app/app.config.js file. Change the value of the **sharepointApi** constant to the server-relative URL of the SharePoint site where you created the Todo list, followed by `/_api/`.</span></span>

### <a name="add-css-styles"></a><span data-ttu-id="91c69-153">Добавление стилей CSS</span><span class="sxs-lookup"><span data-stu-id="91c69-153">Add CSS styles</span></span>

<span data-ttu-id="91c69-154">Кроме того, необходимо реализовать стили CSS, которые вы используете с шаблоном.</span><span class="sxs-lookup"><span data-stu-id="91c69-154">You also need to implement CSS styles that you are using the template. In the code editor open the ToDo.module.scss file and replace its contents with:</span></span> <span data-ttu-id="91c69-155">В редакторе кода откройте файл **ToDoWebPart.module.scss** и замените его содержимое на следующие строки:</span><span class="sxs-lookup"><span data-stu-id="91c69-155">In the code editor open the **IToDoWebPartProps.ts** file and replace its contents with the following:</span></span>

```scss
.toDo {
  .loading {
    margin: 0 auto;
    width: 6em;
  }
}
```

### <a name="trust-the-development-certificate"></a><span data-ttu-id="91c69-156">Доверие сертификату разработки</span><span class="sxs-lookup"><span data-stu-id="91c69-156">Trust the development certificate</span></span>

<span data-ttu-id="91c69-p109">По умолчанию сертификат разработки, необходимый для загрузки рабочей области SharePoint и ее ресурсов по протоколу HTTPS, не является доверенным, и при ее запуске в веб-браузере появляется предупреждение. В некоторых веб-браузерах рабочая область SharePoint не загружается, если SSL-сертификат не является доверенным. Чтобы избежать этой проблемы, следует одобрить сертификат разработки, предоставленный вместе с платформой SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="91c69-p109">By default the development certificate required to load SharePoint workbench and its resources over HTTPS is not trusted and causes the web browser to show a warning when navigating to the SharePoint workbench. In situations when you want to run SharePoint workbench in the context of SharePoint, some web browsers prevent the workbench from loading if the SSL certificate isn't trusted. To avoid this issue you should trust the development certificate provided with the SharePoint Framework.</span></span>

<span data-ttu-id="91c69-160">Выполните в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="91c69-160">In the command line execute:</span></span>

```sh
gulp trust-dev-cert
```

### <a name="preview-web-part-in-the-hosted-workbench"></a><span data-ttu-id="91c69-161">Просмотр веб-части в размещенной системе разработки</span><span class="sxs-lookup"><span data-stu-id="91c69-161">Preview the web part in workbench</span></span>

<span data-ttu-id="91c69-162">Выполните в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="91c69-162">In the command line execute:</span></span>

```sh
gulp serve --nobrowser
```

<span data-ttu-id="91c69-163">К URL-адресу сайта SharePoint добавьте `/_layouts/workbench.aspx`, например</span><span class="sxs-lookup"><span data-stu-id="91c69-163">To the URL of your SharePoint site, add `/_layouts/workbench.aspx`, eg.</span></span> <span data-ttu-id="91c69-164">`https://contoso.sharepoint.com/_layouts/workbench.aspx`, а затем перейдите по этому адресу в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="91c69-164">`https://contoso.sharepoint.com/_layouts/workbench.aspx`, and navigate to it in the web browser.</span></span>

<span data-ttu-id="91c69-165">Если вы правильно выполнили все действия, в браузере должна появиться веб-часть с формой для добавления элементов в список дел.</span><span class="sxs-lookup"><span data-stu-id="91c69-165">If you followed all steps correctly, you should see the web part in the browser showing the form to add to do items.</span></span>

![Перенесенное приложение AngularJS в системе разработки SharePoint (отправлено в SharePoint)](../../../images/ng-migration-first-run.png)

<span data-ttu-id="91c69-167">Добавьте несколько элементов списка дел, чтобы проверить работу веб-части.</span><span class="sxs-lookup"><span data-stu-id="91c69-167">Add a few todo items to verify that the web part is working as expected.</span></span>

![Перенесенное приложение AngularJS с неправильным стилем](../../../images/ng-migration-old-office-ui-fabric.png)

### <a name="fix-web-part-styling"></a><span data-ttu-id="91c69-169">Исправление стиля веб-части</span><span class="sxs-lookup"><span data-stu-id="91c69-169">Fix web part styling</span></span>

<span data-ttu-id="91c69-170">Веб-часть работает правильно, но выглядит не так, как исходное приложение AngularJS.</span><span class="sxs-lookup"><span data-stu-id="91c69-170">Although the web part is working correctly, it doesn't look the same as the AngularJS application you started with.</span></span> <span data-ttu-id="91c69-171">Это связано с тем, что ngOfficeUIFabric использует более раннюю версию Office UI Fabric, чем система разработки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="91c69-171">This is caused because ngOfficeUIFabric uses an older version of Office UI Fabric than the one available in the SharePoint workbench.</span></span> <span data-ttu-id="91c69-172">Ситуацию легко исправить, загрузив стили CSS, используемые в ngOfficeUIFabric.</span><span class="sxs-lookup"><span data-stu-id="91c69-172">The easy fix would be to load the CSS styles used by ngOfficeUIFabric.</span></span> <span data-ttu-id="91c69-173">Но эти стили будут конфликтовать со стилями Office UI Fabric, используемыми в рабочей области SharePoint. В результате изменится ее пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="91c69-173">The problem with that is, that these styles would collide with the Office UI Fabric styles used by the SharePoint workbench, breaking its user interface.</span></span> <span data-ttu-id="91c69-174">Более эффективное решение — добавить стили, необходимые определенным компонентам, к стилям веб-части.</span><span class="sxs-lookup"><span data-stu-id="91c69-174">A better solution is to add the styles required by the specific components to the web part styles.</span></span>

<span data-ttu-id="91c69-175">Откройте в редакторе кода файл **./src/webparts/toDo/ToDoWebPart.module.scss**.</span><span class="sxs-lookup"><span data-stu-id="91c69-175">In the code editor open the **./src/webparts/toDo/ToDoWebPart.ts** file.</span></span> <span data-ttu-id="91c69-176">Замените его содержимое следующим:</span><span class="sxs-lookup"><span data-stu-id="91c69-176">Change its contents to:</span></span>

```scss
.toDo {
  .loading {
    margin: 0 auto;
    width: 6em;
  }

  .done :global .ms-ListItem-primaryText {
    text-decoration: line-through;
  }

  ul, li {
    margin: 0;
    padding: 0;
  }

  :global {
    .ms-Spinner{position:relative;height:20px}.ms-Spinner.ms-Spinner--large{height:28px}.ms-Spinner.ms-Spinner--large .ms-Spinner-label{left:34px;top:6px}.ms-Spinner-circle{position:absolute;border-radius:100px;background-color:#0078d7;opacity:0}@media screen and (-ms-high-contrast:active){.ms-Spinner-circle{background-color:#fff}}@media screen and (-ms-high-contrast:black-on-white){.ms-Spinner-circle{background-color:#000}}.ms-Spinner-label{position:relative;color:#333;font-family:Segoe UI Regular WestEuropean,Segoe UI,Tahoma,Arial,sans-serif;font-size:12px;font-weight:400;color:#0078d7;left:28px;top:2px}
    .ms-TextField{color:#333;font-family:Segoe UI Regular WestEuropean,Segoe UI,Tahoma,Arial,sans-serif;font-size:14px;font-weight:400;box-sizing:border-box;margin:0;padding:0;box-shadow:none;margin-bottom:8px}.ms-TextField.is-disabled .ms-TextField-field{background-color:#f4f4f4;border-color:#f4f4f4;pointer-events:none;cursor:default}.ms-TextField.is-disabled:-moz-placeholder,.ms-TextField.is-disabled:-ms-input-placeholder,.ms-TextField.is-disabled::-moz-placeholder,.ms-TextField.is-disabled::-webkit-input-placeholder{color:#a6a6a6}.ms-TextField.is-required .ms-Label:after{content:' *';color:#a80000}.ms-TextField.is-required:-moz-placeholder:after,.ms-TextField.is-required:-ms-input-placeholder:after,.ms-TextField.is-required::-moz-placeholder:after,.ms-TextField.is-required::-webkit-input-placeholder:after{content:' *';color:#a80000}.ms-TextField.is-active{border-color:#0078d7}.ms-TextField-field{box-sizing:border-box;margin:0;padding:0;box-shadow:none;border:1px solid #c8c8c8;border-radius:0;font-family:Segoe UI Semilight WestEuropean,Segoe UI Semilight,Segoe UI,Tahoma,Arial,sans-serif;font-size:12px;color:#333;height:32px;padding:6px 10px 8px;width:100%;min-width:180px;outline:0}.ms-TextField-field:hover{border-color:#767676}.ms-TextField-field:focus{border-color:#0078d7}@media screen and (-ms-high-contrast:active){.ms-TextField-field:focus,.ms-TextField-field:hover{border-color:#1aebff}}@media screen and (-ms-high-contrast:black-on-white){.ms-TextField-field:focus,.ms-TextField-field:hover{border-color:#37006e}}.ms-TextField-field:-moz-placeholder,.ms-TextField-field:-ms-input-placeholder,.ms-TextField-field::-moz-placeholder,.ms-TextField-field::-webkit-input-placeholder{color:#666}.ms-TextField-description{color:#767676;font-size:11px}.ms-TextField.ms-TextField--placeholder{position:relative}.ms-TextField.ms-TextField--placeholder .ms-Label{position:absolute;font-family:Segoe UI Semilight WestEuropean,Segoe UI Semilight,Segoe UI,Tahoma,Arial,sans-serif;font-size:12px;color:#666;padding:7px 0 7px 10px}.ms-TextField.ms-TextField--placeholder.is-disabled,.ms-TextField.ms-TextField--placeholder.is-disabled .ms-Label{color:#a6a6a6}@media screen and (-ms-high-contrast:active){.ms-TextField.ms-TextField--placeholder.is-disabled .ms-Label{color:#0f0}}@media screen and (-ms-high-contrast:black-on-white){.ms-TextField.ms-TextField--placeholder.is-disabled .ms-Label{color:#600000}}.ms-TextField.ms-TextField--underlined{border-bottom:1px solid #c8c8c8;display:table;width:100%;min-width:180px}.ms-TextField.ms-TextField--underlined:hover{border-color:#767676}@media screen and (-ms-high-contrast:active){.ms-TextField.ms-TextField--underlined:hover{border-color:#1aebff}}@media screen and (-ms-high-contrast:black-on-white){.ms-TextField.ms-TextField--underlined:hover{border-color:#37006e}}.ms-TextField.ms-TextField--underlined:active,.ms-TextField.ms-TextField--underlined:focus{border-color:#0078d7}.ms-TextField.ms-TextField--underlined .ms-Label{font-size:12px;margin-right:8px;display:table-cell;vertical-align:bottom;padding-left:12px;padding-bottom:5px;height:32px;width:1%;white-space:nowrap}.ms-TextField.ms-TextField--underlined .ms-TextField-field{border:0;float:left;display:table-cell;text-align:left;padding-top:8px;padding-bottom:2px}.ms-TextField.ms-TextField--underlined .ms-TextField-field:active,.ms-TextField.ms-TextField--underlined .ms-TextField-field:focus,.ms-TextField.ms-TextField--underlined .ms-TextField-field:hover{outline:0}.ms-TextField.ms-TextField--underlined.is-disabled{border-bottom-color:#eaeaea}.ms-TextField.ms-TextField--underlined.is-disabled .ms-Label{color:#a6a6a6}@media screen and (-ms-high-contrast:active){.ms-TextField.ms-TextField--underlined.is-disabled .ms-Label{color:#0f0}}@media screen and (-ms-high-contrast:black-on-white){.ms-TextField.ms-TextField--underlined.is-disabled .ms-Label{color:#600000}}.ms-TextField.ms-TextField--underlined.is-disabled .ms-TextField-field{background-color:transparent;color:#a6a6a6}.ms-TextField.ms-TextField--underlined.is-active{border-color:#0078d7}@media screen and (-ms-high-contrast:active){.ms-TextField.ms-TextField--underlined.is-active{border-color:#1aebff}}@media screen and (-ms-high-contrast:black-on-white){.ms-TextField.ms-TextField--underlined.is-active{border-color:#37006e}}.ms-TextField.ms-TextField--multiline .ms-TextField-field{line-height:17px;min-height:60px;min-width:260px;padding-top:6px;overflow:auto}.ms-Label,.ms-TextField.ms-TextField--multiline .ms-TextField-field{color:#333;font-family:Segoe UI Regular WestEuropean,Segoe UI,Tahoma,Arial,sans-serif;font-size:12px;font-weight:400}
    .ms-Label{margin:0;padding:0;box-shadow:none;box-sizing:border-box;display:block;padding:5px 0}.ms-Label.is-required:after{content:' *';color:#a80000}.ms-Label.is-disabled{color:#a6a6a6}@media screen and (-ms-high-contrast:active){.ms-Label.is-disabled{color:#0f0}}@media screen and (-ms-high-contrast:black-on-white){.ms-Label.is-disabled{color:#600000}}.is-disabled .ms-Label{color:#a6a6a6}@media screen and (-ms-high-contrast:active){.is-disabled .ms-Label{color:#0f0}}@media screen and (-ms-high-contrast:black-on-white){.is-disabled .ms-Label{color:#600000}}.ms-Toggle{color:#333;font-family:Segoe UI Regular WestEuropean,Segoe UI,Tahoma,Arial,sans-serif;font-size:14px;font-weight:400;box-sizing:border-box;margin:0;padding:0;box-shadow:none;position:relative;display:block;margin-bottom:26px}.ms-Toggle .ms-Label{position:relative;padding:0 0 0 62px;font-size:12px}.ms-Toggle:hover .ms-Label{color:#000}.ms-Toggle:active .ms-Label{color:#333}.ms-Toggle.is-disabled .ms-Label{color:#a6a6a6}@media screen and (-ms-high-contrast:active){.ms-Toggle.is-disabled .ms-Label{color:#0f0}}@media screen and (-ms-high-contrast:black-on-white){.ms-Toggle.is-disabled .ms-Label{color:#600000}}
    .ms-ListItem{font-family:"Segoe UI WestEuropean","Segoe UI",-apple-system,BlinkMacSystemFont,Roboto,"Helvetica Neue",sans-serif;-webkit-font-smoothing:antialiased;font-size:14px;font-weight:400;box-sizing:border-box;margin:0;padding:0;box-shadow:none;padding:9px 28px 3px;position:relative;display:block}.ms-ListItem::after,.ms-ListItem::before{display:table;content:"";line-height:0}.ms-ListItem::after{clear:both}.ms-ListItem-primaryText,.ms-ListItem-secondaryText,.ms-ListItem-tertiaryText{display:block;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;display:block}.ms-ListItem-primaryText{font-family:"Segoe UI WestEuropean","Segoe UI",-apple-system,BlinkMacSystemFont,Roboto,"Helvetica Neue",sans-serif;-webkit-font-smoothing:antialiased;font-size:21px;font-weight:100;padding-right:80px;position:relative;top:-4px}.ms-ListItem-secondaryText{font-family:"Segoe UI WestEuropean","Segoe UI",-apple-system,BlinkMacSystemFont,Roboto,"Helvetica Neue",sans-serif;-webkit-font-smoothing:antialiased;font-size:14px;font-weight:400;line-height:25px;position:relative;top:-7px;padding-right:30px}.ms-ListItem-tertiaryText{font-family:"Segoe UI WestEuropean","Segoe UI",-apple-system,BlinkMacSystemFont,Roboto,"Helvetica Neue",sans-serif;-webkit-font-smoothing:antialiased;font-size:14px;font-weight:400;position:relative;top:-9px;margin-bottom:-4px;padding-right:30px}.ms-ListItem-metaText{font-family:"Segoe UI WestEuropean","Segoe UI",-apple-system,BlinkMacSystemFont,Roboto,"Helvetica Neue",sans-serif;-webkit-font-smoothing:antialiased;font-size:11px;font-weight:400;position:absolute;right:30px;top:39px}.ms-ListItem-image{float:left;height:70px;margin-left:-8px;margin-right:10px;width:70px}.ms-ListItem-selectionTarget{display:none}.ms-ListItem-actions{max-width:80px;position:absolute;right:30px;text-align:right;top:10px}.ms-ListItem-action{color:#a6a6a6;display:inline-block;font-size:15px;position:relative;text-align:center;top:3px;cursor:pointer;height:16px;width:16px}.ms-ListItem-action .ms-Icon{vertical-align:top}.ms-ListItem-action:hover{color:#666666;outline:1px solid transparent}.ms-ListItem.is-unread{border-left:3px solid #0078d7;padding-left:27px}.ms-ListItem.is-unread .ms-ListItem-metaText,.ms-ListItem.is-unread .ms-ListItem-secondaryText{color:#0078d7;font-weight:600}.ms-ListItem.is-unseen:after{border-right:10px solid transparent;border-top:10px solid #0078d7;left:0;position:absolute;top:0}.ms-ListItem.is-selectable .ms-ListItem-selectionTarget{display:block;height:20px;left:6px;position:absolute;top:13px;width:20px}.ms-ListItem.is-selectable .ms-ListItem-image{margin-left:0}.ms-ListItem.is-selectable:hover{background-color:#eaeaea;cursor:pointer;outline:1px solid transparent}.ms-ListItem.is-selectable:hover:before{-moz-osx-font-smoothing:grayscale;-webkit-font-smoothing:antialiased;display:inline-block;font-family:FabricMDL2Icons;font-style:normal;font-weight:400;speak:none;position:absolute;top:12px;left:6px;height:15px;width:15px;border:1px solid #767676}.ms-ListItem.is-selected:before{border:1px solid transparent}.ms-ListItem.is-selected:before,.ms-ListItem.is-selected:hover:before{-moz-osx-font-smoothing:grayscale;-webkit-font-smoothing:antialiased;display:inline-block;font-family:FabricMDL2Icons;font-style:normal;font-weight:400;speak:none;content:'\e041';font-size:15px;color:#767676;position:absolute;top:12px;left:6px}.ms-ListItem.is-selected:hover{background-color:#c7e0f4;outline:1px solid transparent}.ms-ListItem.ms-ListItem--document{padding:0}.ms-ListItem.ms-ListItem--document .ms-ListItem-itemIcon{width:70px;height:70px;float:left;text-align:center}.ms-ListItem.ms-ListItem--document .ms-ListItem-itemIcon .ms-Icon{font-size:38px;line-height:70px;color:#666666}.ms-ListItem.ms-ListItem--document .ms-ListItem-primaryText{display:block;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:14px;padding-top:15px;padding-right:0;position:static}.ms-ListItem.ms-ListItem--document .ms-ListItem-secondaryText{display:block;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-family:"Segoe UI WestEuropean","Segoe UI",-apple-system,BlinkMacSystemFont,Roboto,"Helvetica Neue",sans-serif;-webkit-font-smoothing:antialiased;font-size:11px;font-weight:400;padding-top:6px}.MailList{overflow-y:auto;-webkit-overflow-scrolling:touch;max-height:500px}.MailTile{margin-bottom:5px;padding:10px;background:red}
  }
}
```

<span data-ttu-id="91c69-177">В файле **./src/webparts/toDo/ToDoWebPart.ts** найдите метод **render** и измените шаблон отрисовки приложения так, чтобы использовались новые значки Office UI Fabric.</span><span class="sxs-lookup"><span data-stu-id="91c69-177">In the **./src/webparts/toDo/ToDoWebPart.ts** file, in the **render** method change the application rendering template to use new Office UI Fabric icons.</span></span>

```ts
export default class ToDoWebPart extends BaseClientSideWebPart<IToDoWebPartProps> {
  // ...
  public render(): void {
    if (this.renderedOnce === false) {
      require('./app/app.module');
      require('./app/app.config');
      require('./app/data.service');
      require('./app/home.controller');

      this.domElement.innerHTML = `
        <div class="${styles.toDo}">
          <div data-ng-controller="homeController as vm">
            <div class="${styles.loading}" ng-show="vm.isLoading">
              <uif-spinner>Loading...</uif-spinner>
            </div>
            <div id="entryform" ng-show="vm.isLoading === false">
              <uif-textfield uif-label="New to do:" uif-underlined ng-model="vm.newItem" ng-keydown="vm.todoKeyDown($event)"></uif-textfield>
            </div>
            <uif-list id="items" ng-show="vm.isLoading === false" >
              <uif-list-item ng-repeat="todo in vm.todoCollection" uif-item="todo" ng-class="{'${styles.done}': todo.done}">
                <uif-list-item-primary-text>{{todo.title}}</uif-list-item-primary-text>
                <uif-list-item-actions>
                  <uif-list-item-action ng-click="vm.completeTodo(todo)" ng-show="todo.done === false">
                    <i class="ms-Icon ms-Icon--CheckMark" aria-hidden="true"></i>
                  </uif-list-item-action>
                  <uif-list-item-action ng-click="vm.undoTodo(todo)" ng-show="todo.done">
                    <i class="ms-Icon ms-Icon--RevToggleKey" aria-hidden="true"></i>
                  </uif-list-item-action>
                  <uif-list-item-action ng-click="vm.deleteTodo(todo)">
                    <i class="ms-Icon ms-Icon--Delete" aria-hidden="true"></i>
                  </uif-list-item-action>
                </uif-list-item-actions>
              </uif-list-item>
            </uif-list>
          </div>
        </div>`;

      angular.bootstrap(this.domElement, ['todoapp']);
    }
  }
  // ...
}
```

<span data-ttu-id="91c69-178">Когда вы обновите страницу веб-части в браузере, стиль станет правильным.</span><span class="sxs-lookup"><span data-stu-id="91c69-178">If you refresh the web part in the web browser, you will see that it is now correctly styled.</span></span>

![Перенесенное приложение AngularJS с правильной пометкой выполненных задач в веб-части](../../../images/ng-migration-correct-styling.png)

## <a name="upgrade-the-angularjs-application-to-typescript"></a><span data-ttu-id="91c69-180">Обновление приложения AngularJS до TypeScript</span><span class="sxs-lookup"><span data-stu-id="91c69-180">Upgrade the Angular application to TypeScript</span></span>

<span data-ttu-id="91c69-181">Исходное приложение AngularJS написано на обычном JavaScript, из-за чего в нем могут возникать ошибки.</span><span class="sxs-lookup"><span data-stu-id="91c69-181">The original AngularJS application is written in plain JavaScript which makes maintaining it error-prone.</span></span> <span data-ttu-id="91c69-182">При создании клиентских веб-частей на платформе SharePoint Framework можно использовать TypeScript и его функции обеспечения безопасности типа во время разработки.</span><span class="sxs-lookup"><span data-stu-id="91c69-182">When building SharePoint Framework client-side web parts you can use TypeScript and benefit of its design-time type safety features.</span></span> <span data-ttu-id="91c69-183">На этом этапе мы преобразуем обычный код JavaScript AngularJS в TypeScript.</span><span class="sxs-lookup"><span data-stu-id="91c69-183">In this part of this you will migrate the plain JavaScript AngularJS code to TypeScript.</span></span>

### <a name="upgrade-application-configuration"></a><span data-ttu-id="91c69-184">Обновление конфигурации приложения</span><span class="sxs-lookup"><span data-stu-id="91c69-184">Upgrade application configuration</span></span>

<span data-ttu-id="91c69-185">В проекте переименуйте файл **./src/webparts/toDo/app/app.config.js** в `app.config.ts`.</span><span class="sxs-lookup"><span data-stu-id="91c69-185">In your project rename the ./src/webparts/toDo/app/app.config.js file to . Change its contents to:</span></span> <span data-ttu-id="91c69-186">Измените его содержимое на следующее:</span><span class="sxs-lookup"><span data-stu-id="91c69-186">Change its contents to:</span></span>

```ts
import * as angular from 'angular';

export default function() {
  const todoapp: ng.IModule = angular.module('todoapp');
  todoapp.constant('sharepointApi', '/todo/_api/');
  todoapp.constant('todoListName', 'Todo');
  todoapp.constant('hideFinishedTasks', false);
}
```

### <a name="upgrade-data-service"></a><span data-ttu-id="91c69-187">Обновление службы данных</span><span class="sxs-lookup"><span data-stu-id="91c69-187">Upgrade data service</span></span>

<span data-ttu-id="91c69-188">В проекте переименуйте файл **./src/webparts/toDo/app/data.service.js** в `DataService.ts`.</span><span class="sxs-lookup"><span data-stu-id="91c69-188">In your project rename the ./src/webparts/toDo/app/data.service.js file to . Change its contents to:</span></span> <span data-ttu-id="91c69-189">Измените его содержимое на следующее:</span><span class="sxs-lookup"><span data-stu-id="91c69-189">Change its contents to:</span></span>

```ts
import * as angular from 'angular';

export interface ITodo {
  id: number;
  title: string;
  done: boolean;
}

interface ITodoItem {
  Id: number;
  Title: string;
  Status: string;
}

export interface IDataService {
  getTodos: () => angular.IPromise<ITodo[]>;
  addTodo: (todo: string) => angular.IPromise<{}>;
  deleteTodo: (todo: ITodo) => angular.IPromise<{}>;
  setTodoStatus: (todo: ITodo, done: boolean) => angular.IPromise<{}>;
}

export default class DataService implements IDataService {
  public static $inject: string[] = ['$q', '$http', 'sharepointApi', 'todoListName', 'hideFinishedTasks'];

  constructor(private $q: angular.IQService,
    private $http: angular.IHttpService,
    private sharepointApi: string,
    private todoListName: string,
    private hideFinishedTasks: boolean) {
  }

  public getTodos(): angular.IPromise<ITodo[]> {
    const deferred: angular.IDeferred<ITodo[]> = this.$q.defer();

    let url: string = `${this.sharepointApi}web/lists/getbytitle('${this.todoListName}')/items?$select=Id,Title,Status&$orderby=ID desc`;

    if (this.hideFinishedTasks === true) {
      url += "&$filter=Status ne 'Completed'";
    }

    this.$http({
      url: url,
      method: 'GET',
      headers: {
        'Accept': 'application/json;odata=nometadata'
      }
    }).then((result: angular.IHttpPromiseCallbackArg<{ value: ITodoItem[] }>): void => {
      const todos: ITodo[] = [];
      for (let i: number = 0; i < result.data.value.length; i++) {
        const todo: ITodoItem = result.data.value[i];
        todos.push({
          id: todo.Id,
          title: todo.Title,
          done: todo.Status === 'Completed'
        });
      }
      deferred.resolve(todos);
    });

    return deferred.promise;
  }

  public addTodo(todo: string): angular.IPromise<{}> {
    const deferred: angular.IDeferred<{}> = this.$q.defer();

    let listItemEntityTypeFullName: string = undefined;
    this.getListItemEntityTypeFullName()
      .then((entityTypeName: string): angular.IPromise<string> => {
        listItemEntityTypeFullName = entityTypeName;
        return this.getRequestDigest();
      })
      .then((requestDigest: string): void => {
        const body: string = JSON.stringify({
          '__metadata': { 'type': listItemEntityTypeFullName },
          'Title': todo
        });
        this.$http({
          url: `${this.sharepointApi}web/lists/getbytitle('${this.todoListName}')/items`,
          method: 'POST',
          headers: {
            'Accept': 'application/json;odata=nometadata',
            'Content-type': 'application/json;odata=verbose',
            'X-RequestDigest': requestDigest
          },
          data: body
        }).then((result: angular.IHttpPromiseCallbackArg<{}>): void => {
          deferred.resolve();
        });
      });

    return deferred.promise;
  }

  public deleteTodo(todo: ITodo): angular.IPromise<{}> {
    const deferred: angular.IDeferred<{}> = this.$q.defer();

    this.getRequestDigest()
      .then((requestDigest: string): void => {
        this.$http({
          url: `${this.sharepointApi}web/lists/getbytitle('${this.todoListName}')/items(${todo.id})`,
          method: 'POST',
          headers: {
            'Accept': 'application/json;odata=nometadata',
            'X-RequestDigest': requestDigest,
            'IF-MATCH': '*',
            'X-HTTP-Method': 'DELETE'
          }
        }).then((result: angular.IHttpPromiseCallbackArg<{}>): void => {
          deferred.resolve();
        });
      });

    return deferred.promise;
  }

  public setTodoStatus(todo: ITodo, done: boolean): angular.IPromise<{}> {
    const deferred: angular.IDeferred<{}> = this.$q.defer();

    let listItemEntityTypeFullName: string = undefined;
    this.getListItemEntityTypeFullName()
      .then((entityTypeName: string): angular.IPromise<string> => {
        listItemEntityTypeFullName = entityTypeName;
        return this.getRequestDigest();
      })
      .then((requestDigest: string): void => {
        const body: string = JSON.stringify({
          '__metadata': { 'type': listItemEntityTypeFullName },
          'Status': done ? 'Completed' : 'Not started'
        });
        this.$http({
          url: `${this.sharepointApi}web/lists/getbytitle('${this.todoListName}')/items(${todo.id})`,
          method: 'POST',
          headers: {
            'Accept': 'application/json;odata=nometadata',
            'Content-type': 'application/json;odata=verbose',
            'X-RequestDigest': requestDigest,
            'IF-MATCH': '*',
            'X-HTTP-Method': 'MERGE'
          },
          data: body
        }).then((result: angular.IHttpPromiseCallbackArg<{}>): void => {
          deferred.resolve();
        });
      });

    return deferred.promise;
  }

  private getRequestDigest(): angular.IPromise<string> {
    const deferred: angular.IDeferred<string> = this.$q.defer();

    this.$http({
      url: this.sharepointApi + 'contextinfo',
      method: 'POST',
      headers: {
        'Accept': 'application/json;odata=nometadata'
      }
    }).then((result: angular.IHttpPromiseCallbackArg<{ FormDigestValue: string }>): void => {
      deferred.resolve(result.data.FormDigestValue);
    }, (err: any): void => {
      deferred.reject(err);
    });

    return deferred.promise;
  }

  private getListItemEntityTypeFullName(): angular.IPromise<string> {
    const deferred: angular.IDeferred<string> = this.$q.defer();

    this.$http({
      url: `${this.sharepointApi}web/lists/getbytitle('${this.todoListName}')?$select=ListItemEntityTypeFullName`,
      method: 'GET',
      headers: {
        'Accept': 'application/json;odata=nometadata'
      }
    }).then((result: angular.IHttpPromiseCallbackArg<{ ListItemEntityTypeFullName: string }>): void => {
      deferred.resolve(result.data.ListItemEntityTypeFullName);
    }, (err: any): void => {
      deferred.reject(err);
    });

    return deferred.promise;
  }
}
```

### <a name="upgrade-home-controller"></a><span data-ttu-id="91c69-190">Обновление контроллера домашней страницы</span><span class="sxs-lookup"><span data-stu-id="91c69-190">Upgrade home controller</span></span>

<span data-ttu-id="91c69-191">В проекте переименуйте файл **./src/webparts/toDo/app/home.controller.js** в `HomeController.ts`.</span><span class="sxs-lookup"><span data-stu-id="91c69-191">In your project rename the ./src/webparts/toDo/app/home.controller.js file to . Change its contents to:</span></span> <span data-ttu-id="91c69-192">Измените его содержимое на следующее:</span><span class="sxs-lookup"><span data-stu-id="91c69-192">Change its contents to:</span></span>

```ts
import * as angular from 'angular';
import { IDataService, ITodo } from './DataService';

export default class HomeController {
  public isLoading: boolean = false;
  public newItem: string = null;
  public todoCollection: ITodo[] = [];

  public static $inject: string[] = ['DataService', '$window'];

  constructor(private dataService: IDataService, private $window: angular.IWindowService) {
    this.loadTodos();
  }

  private loadTodos(): void {
    this.isLoading = true;
    this.dataService.getTodos()
      .then((todos: ITodo[]): void => {
        this.todoCollection = todos;
      })
      .finally((): void => {
        this.isLoading = false;
      });
  }

  public todoKeyDown($event: KeyboardEvent): void {
    if ($event.keyCode === 13 && this.newItem.length > 0) {
      $event.preventDefault();

      this.todoCollection.unshift({ id: -1, title: this.newItem, done: false });

      this.dataService.addTodo(this.newItem)
        .then((): void => {
          this.newItem = null;
          this.dataService.getTodos()
            .then((todos: ITodo[]): void => {
              this.todoCollection = todos;
            });
        });
    }
  }

  public deleteTodo(todo: ITodo): void {
    if (this.$window.confirm('Are you sure you want to delete this todo item?')) {
      let index: number = -1;
      for (let i: number = 0; i < this.todoCollection.length; i++) {
        if (this.todoCollection[i].id === todo.id) {
          index = i;
          break;
        }
      }

      if (index > -1) {
        this.todoCollection.splice(index, 1);
      }

      this.dataService.deleteTodo(todo)
        .then((): void => {
          this.dataService.getTodos()
            .then((todos: ITodo[]): void => {
              this.todoCollection = todos;
            });
        });
    }
  }

  public completeTodo(todo: ITodo): void {
    todo.done = true;

    this.dataService.setTodoStatus(todo, true)
      .then((): void => {
        this.dataService.getTodos()
          .then((todos: ITodo[]): void => {
            this.todoCollection = todos;
          });
      });
  }

  public undoTodo(todo: ITodo): void {
    todo.done = false;

    this.dataService.setTodoStatus(todo, false)
      .then((): void => {
        this.dataService.getTodos()
          .then((todos: ITodo[]): void => {
            this.todoCollection = todos;
          });
      });
  }
}
```

### <a name="upgrade-application-module"></a><span data-ttu-id="91c69-193">Обновление модуля приложения</span><span class="sxs-lookup"><span data-stu-id="91c69-193">Upgrade application module</span></span>

<span data-ttu-id="91c69-194">В проекте переименуйте файл **./src/webparts/toDo/app/app.module.js** в `app.module.ts`.</span><span class="sxs-lookup"><span data-stu-id="91c69-194">In your project rename the ./src/webparts/toDo/app/app.module.js file to . Change its contents to:</span></span> <span data-ttu-id="91c69-195">Замените его содержимое следующим:</span><span class="sxs-lookup"><span data-stu-id="91c69-195">Change its contents to:</span></span>

```ts
import * as angular from 'angular';
import config from './app.config';
import HomeController from './HomeController';
import DataService from './DataService';

import 'ng-office-ui-fabric';

const todoapp: angular.IModule = angular.module('todoapp', [
  'officeuifabric.core',
  'officeuifabric.components'
]);

config();

todoapp
  .controller('HomeController', HomeController)
  .service('DataService', DataService);
```

### <a name="update-reference-to-angularjs-application-in-the-web-part"></a><span data-ttu-id="91c69-196">Обновление ссылки на приложение AngularJS в веб-части</span><span class="sxs-lookup"><span data-stu-id="91c69-196">Update reference to Angular application in the web part</span></span>

<span data-ttu-id="91c69-197">Теперь, когда приложение AngularJS написано на TypeScript, а его фрагменты ссылаются друг на друга, веб-части больше не требуется ссылаться на все фрагменты приложения.</span><span class="sxs-lookup"><span data-stu-id="91c69-197">Now that the Angular application is built using TypeScript and its different pieces reference each other, it's no longer necessary for the web part to reference all pieces of the application. Instead it only needs to load the main module, which in result will load all other elements that build up the Angular application.</span></span> <span data-ttu-id="91c69-198">Ей достаточно загрузить главный модуль, который загрузит все остальные элементы приложения AngularJS.</span><span class="sxs-lookup"><span data-stu-id="91c69-198">Instead it only needs to load the main module, which in result will load all other elements that build up the AngularJS application.</span></span>

<span data-ttu-id="91c69-199">В редакторе кода откройте файл **./src/webparts/toDo/ToDoWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="91c69-199">In the code editor open the **./src/webparts/toDo/ToDoWebPart.ts** file.</span></span> <span data-ttu-id="91c69-200">Замените метод **render** следующим:</span><span class="sxs-lookup"><span data-stu-id="91c69-200">Change the **render** method to:</span></span>

```ts
export default class ToDoWebPart extends BaseClientSideWebPart<IToDoWebPartProps> {
  // ...
  public render(): void {
    if (this.renderedOnce === false) {
      require('./app/app.module');

      this.domElement.innerHTML = `
        <div class="${styles.toDo}">
          <div data-ng-controller="HomeController as vm">
            <div class="${styles.loading}" ng-show="vm.isLoading">
              <uif-spinner>Loading...</uif-spinner>
            </div>
            <div id="entryform" ng-show="vm.isLoading === false">
              <uif-textfield uif-label="New to do:" uif-underlined ng-model="vm.newItem" ng-keydown="vm.todoKeyDown($event)"></uif-textfield>
            </div>
            <uif-list id="items" ng-show="vm.isLoading === false" >
              <uif-list-item ng-repeat="todo in vm.todoCollection" uif-item="todo" ng-class="{'${styles.done}': todo.done}">
                <uif-list-item-primary-text>{{todo.title}}</uif-list-item-primary-text>
                <uif-list-item-actions>
                  <uif-list-item-action ng-click="vm.completeTodo(todo)" ng-show="todo.done === false">
                    <i class="ms-Icon ms-Icon--CheckMark" aria-hidden="true"></i>
                  </uif-list-item-action>
                  <uif-list-item-action ng-click="vm.undoTodo(todo)" ng-show="todo.done">
                    <i class="ms-Icon ms-Icon--RevToggleKey" aria-hidden="true"></i>
                  </uif-list-item-action>
                  <uif-list-item-action ng-click="vm.deleteTodo(todo)">
                    <i class="ms-Icon ms-Icon--Delete" aria-hidden="true"></i>
                  </uif-list-item-action>
                </uif-list-item-actions>
              </uif-list-item>
            </uif-list>
          </div>
        </div>`;

      angular.bootstrap(this.domElement, ['todoapp']);
    }
  }
  // ...
}
```

<span data-ttu-id="91c69-201">Чтобы убедиться, что код успешно обновлен до TypeScript, выполните в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="91c69-201">To verify that the upgrade to TypeScript has been successful, in the command line run</span></span>

```sh
gulp serve --nobrowser
```

<span data-ttu-id="91c69-202">Обновите страницу системы разработки SharePoint в веб-браузере. Веб-часть должна отображаться так же, как и раньше.</span><span class="sxs-lookup"><span data-stu-id="91c69-202">In the web browser refresh the SharePoint workbench which should display your web part just as previously.</span></span>

![Перенесенное приложение AngularJS с правильной пометкой выполненных задач в веб-части](../../../images/ng-migration-correct-styling.png)

<span data-ttu-id="91c69-p120">Внешний вид веб-части не изменился, но ее код стал лучше. Если вы захотите ее обновить, вам будет проще проверять правильность и целостность кода во время разработки.</span><span class="sxs-lookup"><span data-stu-id="91c69-p120">Even though the way the web part works hasn't changed, your code is improved. In case of a future update you can more easily verify the correctness and integrity of your code already during development.</span></span>

## <a name="improve-integration-of-the-angularjs-application-with-the-sharepoint-framework"></a><span data-ttu-id="91c69-206">Улучшение интеграции приложения AngularJS с платформой SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="91c69-206">Improve integration of the Angular application with the SharePoint Framework</span></span>

<span data-ttu-id="91c69-207">На этом этапе приложение AngularJS работает правильно и заключено в клиентскую веб-часть на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="91c69-207">At this point the AngularJS application works correctly and is wrapped in a SharePoint Framework client-side web part.</span></span> <span data-ttu-id="91c69-208">Пользователи могут добавить веб-часть на страницу, но не могут настроить ее работу.</span><span class="sxs-lookup"><span data-stu-id="91c69-208">While users can add the web part to the page, they cannot however configure how the web part should work.</span></span> <span data-ttu-id="91c69-209">Все значения конфигурации внедрены в код приложения AngularJS.</span><span class="sxs-lookup"><span data-stu-id="91c69-209">All of the configuration is embedded in the AngularJS application's code.</span></span> <span data-ttu-id="91c69-210">В этом разделе показано расширение веб-части, позволяющее пользователям указывать имя списка дел и управлять отображением выполненных задач.</span><span class="sxs-lookup"><span data-stu-id="91c69-210">At this point the Angular application works correctly and is wrapped in a SharePoint Framework client-side web part. While users can add the web part to the page, they cannot however configure how the web part should work. All of the configuration is embedded in the Angular application's code. In this section you will extend the web part to allow configuration of the name of the list where the todo items are stored and whether the web part should show finished tasks or not.</span></span>

### <a name="define-web-part-properties"></a><span data-ttu-id="91c69-211">Определение свойств веб-части</span><span class="sxs-lookup"><span data-stu-id="91c69-211">Define web part properties</span></span>

<span data-ttu-id="91c69-212">В редакторе кода откройте файл **./src/webparts/toDo/ToDoWebPart.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="91c69-212">In the code editor open the **./src/webparts/toDo/ToDoWebPart.manifest.json** file. Change the properties section to:</span></span> <span data-ttu-id="91c69-213">Замените раздел **properties** следующим:</span><span class="sxs-lookup"><span data-stu-id="91c69-213">Change the **properties** section to:</span></span>

```json
"properties": {
  "todoListName": "Todo",
  "hideFinishedTasks": false
}
```

<span data-ttu-id="91c69-214">В файле **./src/webparts/toDo/ToDoWebPart.ts** замените определение интерфейса `IToDoWebPartProps` следующим:</span><span class="sxs-lookup"><span data-stu-id="91c69-214">In the **./src/webparts/toDo/ToDoWebPart.ts** file, change the definition of the `IToDoWebPartProps` interface to:</span></span>

```ts
export interface IToDoWebPartProps {
  todoListName: string;
  hideFinishedTasks: boolean;
}
```

<span data-ttu-id="91c69-215">В файле **./src/webparts/toDo/ToDoWebPart.ts** замените первый оператор импорта на следующий:</span><span class="sxs-lookup"><span data-stu-id="91c69-215">In the **./src/webparts/toDo/ToDoWebPart.ts** file change the first import statement to:</span></span>

```ts
import {
  BaseClientSideWebPart,
  IPropertyPaneSettings,
  PropertyPaneTextField,
  PropertyPaneToggle
} from '@microsoft/sp-webpart-base';
```

<span data-ttu-id="91c69-216">После этого в файле примера измените замените метод **getPropertyPaneConfiguration** следующим:</span><span class="sxs-lookup"><span data-stu-id="91c69-216">Next, in the same file, change the **getPropertyPaneConfiguration** method to:</span></span>

```ts
export default class ToDoWebPart extends BaseClientSideWebPart<IToDoWebPartProps> {
  // ...
  protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
    return {
      pages: [
        {
          header: {
            description: strings.PropertyPaneDescription
          },
          groups: [
            {
              groupName: strings.BasicGroupName,
              groupFields: [
                PropertyPaneTextField('todoListName', {
                  label: strings.ListNameFieldLabel
                }),
                PropertyPaneToggle('hideFinishedTasks', {
                  label: strings.HideFinishedTasksFieldLabel
                })
              ]
            }
          ]
        }
      ]
    };
  }
  // ...
}
```

<span data-ttu-id="91c69-217">Добавьте недостающие строки ресурсов, заменив содержимое файла **./src/webparts/toDo/loc/mystrings.d.ts** на следующее:</span><span class="sxs-lookup"><span data-stu-id="91c69-217">Add the missing resource strings, by changing the **./src/webparts/toDo/loc/mystrings.d.ts** file contents to:</span></span>

```ts
declare interface IToDoWebPartStrings {
  PropertyPaneDescription: string;
  BasicGroupName: string;
  ListNameFieldLabel: string;
  HideFinishedTasksFieldLabel: string;
}

declare module 'ToDoWebPartStrings' {
  const strings: IToDoWebPartStrings;
  export = strings;
}
```

<span data-ttu-id="91c69-218">В файле **./src/webparts/toDo/loc/en-us.js** добавьте переводы для новых строк:</span><span class="sxs-lookup"><span data-stu-id="91c69-218">In the **./src/webparts/toDo/loc/en-us.js** file add translations for the newly added strings:</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Description",
    "BasicGroupName": "Group Name",
    "ListNameFieldLabel": "List name",
    "HideFinishedTasksFieldLabel": "Hide finished tasks"
  }
});
```

### <a name="pass-web-part-properties-values-to-the-angularjs-application"></a><span data-ttu-id="91c69-219">Передача значений свойств веб-части в приложение AngularJS</span><span class="sxs-lookup"><span data-stu-id="91c69-219">Pass web part properties values to the Angular application</span></span>

<span data-ttu-id="91c69-220">На этом этапе пользователи могут настраивать работу веб-части, но приложение AngularJS не использует эти значения.</span><span class="sxs-lookup"><span data-stu-id="91c69-220">At this moment users can configure how the web part should work, but the AngularJS application isn't using these values.</span></span> <span data-ttu-id="91c69-221">В этом разделе мы расширим приложение AngularJS, чтобы оно использовало значения конфигурации, указанные пользователем в области свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="91c69-221">In this section you will extend the AngularJS application to use the configuration values provided by users through the web part property pane.</span></span> <span data-ttu-id="91c69-222">Для этого можно транслировать событие AngularJS в методе **render** и подписаться на это событие в контроллере, используемом веб-частью.</span><span class="sxs-lookup"><span data-stu-id="91c69-222">One way to do that is to broadcast an AngularJS event in the **render** method and subscribe to this event in the controller used in the web part.</span></span>

#### <a name="delete-angularjs-configuration-file"></a><span data-ttu-id="91c69-223">Удаление файла конфигурации AngularJS</span><span class="sxs-lookup"><span data-stu-id="91c69-223">Delete Angular configuration file</span></span>

<span data-ttu-id="91c69-224">Удалите из проекта файл **./src/webparts/toDo/app/app.config.ts**.</span><span class="sxs-lookup"><span data-stu-id="91c69-224">In your project delete the **./src/webparts/toDo/app/app.config.ts** file.</span></span> <span data-ttu-id="91c69-225">Позже мы обновим приложение, чтобы оно получало значения конфигурации из свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="91c69-225">In your project delete the ./src/webparts/toDo/app/app.config.ts file. In the following steps you will update the application to get the configuration values from web part properties.</span></span>

#### <a name="remove-reference-to-configuration"></a><span data-ttu-id="91c69-226">Удаление ссылки на конфигурацию</span><span class="sxs-lookup"><span data-stu-id="91c69-226">Remove reference to configuration</span></span>

<span data-ttu-id="91c69-227">В файле **./src/webparts/toDo/app/app.module.ts** удалите ссылку на конфигурацию AngularJS, заменив его содержимое следующим:</span><span class="sxs-lookup"><span data-stu-id="91c69-227">In the **./src/webparts/toDo/app/app.module.ts** file remove the reference to the Angular configuration by changing its contents to:</span></span>

```ts
import * as angular from 'angular';
import HomeController from './HomeController';
import DataService from './DataService';

import 'ng-office-ui-fabric';

const todoapp: angular.IModule = angular.module('todoapp', [
  'officeuifabric.core',
  'officeuifabric.components'
]);

todoapp
  .controller('HomeController', HomeController)
  .service('DataService', DataService);
```

#### <a name="update-data-service-to-accept-configuration-value-in-method-parameters"></a><span data-ttu-id="91c69-228">Обновление службы данных для принятия значений конфигурации в параметрах методов</span><span class="sxs-lookup"><span data-stu-id="91c69-228">Update data service to accept configuration value in method parameters</span></span>

<span data-ttu-id="91c69-229">Изначально служба данных получала свою конфигурацию из констант, определенных в файле **app.config.ts**.</span><span class="sxs-lookup"><span data-stu-id="91c69-229">Originally the data service retrieved its configuration from the constants defined in the **app.config.ts** file. In order to use the configuration values configured in web part properties instead, the specific methods must accept parameters.</span></span> <span data-ttu-id="91c69-230">Чтобы использовать вместо них значения конфигурации, настроенные в свойствах веб-части, определенные методы должны принимать параметры.</span><span class="sxs-lookup"><span data-stu-id="91c69-230">Originally the data service retrieved its configuration from the constants defined in the app.config.ts file. In order to use the configuration values configured in web part properties instead, the specific methods must accept parameters.</span></span>

<span data-ttu-id="91c69-231">Откройте в редакторе кода файл **./src/webparts/toDo/app/DataService.ts** и замените его содержимое на следующее:</span><span class="sxs-lookup"><span data-stu-id="91c69-231">In the code editor open the **./src/webparts/toDo/app/DataService.ts** file and change its contents to:</span></span>

```ts
import * as angular from 'angular';

export interface ITodo {
  id: number;
  title: string;
  done: boolean;
}

interface ITodoItem {
  Id: number;
  Title: string;
  Status: string;
}

export interface IDataService {
  getTodos: (sharePointApi: string, todoListName: string, hideFinishedTasks: boolean) => angular.IPromise<ITodo[]>;
  addTodo: (todo: string, sharePointApi: string, todoListName: string) => angular.IPromise<{}>;
  deleteTodo: (todo: ITodo, sharePointApi: string, todoListName: string) => angular.IPromise<{}>;
  setTodoStatus: (todo: ITodo, done: boolean, sharePointApi: string, todoListName: string) => angular.IPromise<{}>;
}

export default class DataService implements IDataService {
  public static $inject: string[] = ['$q', '$http'];

  constructor(private $q: angular.IQService, private $http: angular.IHttpService) {
  }

  public getTodos(sharePointApi: string, todoListName: string, hideFinishedTasks: boolean): angular.IPromise<ITodo[]> {
    const deferred: angular.IDeferred<ITodo[]> = this.$q.defer();

    let url: string = `${sharePointApi}web/lists/getbytitle('${todoListName}')/items?$select=Id,Title,Status&$orderby=ID desc`;

    if (hideFinishedTasks === true) {
      url += "&$filter=Status ne 'Completed'";
    }

    this.$http({
      url: url,
      method: 'GET',
      headers: {
        'Accept': 'application/json;odata=nometadata'
      }
    }).then((result: angular.IHttpPromiseCallbackArg<{ value: ITodoItem[] }>): void => {
      const todos: ITodo[] = [];
      for (let i: number = 0; i < result.data.value.length; i++) {
        const todo: ITodoItem = result.data.value[i];
        todos.push({
          id: todo.Id,
          title: todo.Title,
          done: todo.Status === 'Completed'
        });
      }
      deferred.resolve(todos);
    });

    return deferred.promise;
  }

  public addTodo(todo: string, sharePointApi: string, todoListName: string): angular.IPromise<{}> {
    const deferred: angular.IDeferred<{}> = this.$q.defer();

    let listItemEntityTypeFullName: string = undefined;
    this.getListItemEntityTypeFullName(sharePointApi, todoListName)
      .then((entityTypeName: string): angular.IPromise<string> => {
        listItemEntityTypeFullName = entityTypeName;
        return this.getRequestDigest(sharePointApi);
      })
      .then((requestDigest: string): void => {
        const body: string = JSON.stringify({
          '__metadata': { 'type': listItemEntityTypeFullName },
          'Title': todo
        });
        this.$http({
          url: `${sharePointApi}web/lists/getbytitle('${todoListName}')/items`,
          method: 'POST',
          headers: {
            'Accept': 'application/json;odata=nometadata',
            'Content-type': 'application/json;odata=verbose',
            'X-RequestDigest': requestDigest
          },
          data: body
        }).then((result: angular.IHttpPromiseCallbackArg<{}>): void => {
          deferred.resolve();
        });
      });

    return deferred.promise;
  }

  public deleteTodo(todo: ITodo, sharePointApi: string, todoListName: string): angular.IPromise<{}> {
    const deferred: angular.IDeferred<{}> = this.$q.defer();

    this.getRequestDigest(sharePointApi)
      .then((requestDigest: string): void => {
        this.$http({
          url: `${sharePointApi}web/lists/getbytitle('${todoListName}')/items(${todo.id})`,
          method: 'POST',
          headers: {
            'Accept': 'application/json;odata=nometadata',
            'X-RequestDigest': requestDigest,
            'IF-MATCH': '*',
            'X-HTTP-Method': 'DELETE'
          }
        }).then((result: angular.IHttpPromiseCallbackArg<{}>): void => {
          deferred.resolve();
        });
      });

    return deferred.promise;
  }

  public setTodoStatus(todo: ITodo, done: boolean, sharePointApi: string, todoListName: string): angular.IPromise<{}> {
    const deferred: angular.IDeferred<{}> = this.$q.defer();

    let listItemEntityTypeFullName: string = undefined;
    this.getListItemEntityTypeFullName(sharePointApi, todoListName)
      .then((entityTypeName: string): angular.IPromise<string> => {
        listItemEntityTypeFullName = entityTypeName;
        return this.getRequestDigest(sharePointApi);
      })
      .then((requestDigest: string): void => {
        const body: string = JSON.stringify({
          '__metadata': { 'type': listItemEntityTypeFullName },
          'Status': done ? 'Completed' : 'Not started'
        });
        this.$http({
          url: `${sharePointApi}web/lists/getbytitle('${todoListName}')/items(${todo.id})`,
          method: 'POST',
          headers: {
            'Accept': 'application/json;odata=nometadata',
            'Content-type': 'application/json;odata=verbose',
            'X-RequestDigest': requestDigest,
            'IF-MATCH': '*',
            'X-HTTP-Method': 'MERGE'
          },
          data: body
        }).then((result: angular.IHttpPromiseCallbackArg<{}>): void => {
          deferred.resolve();
        });
      });

    return deferred.promise;
  }

  private getRequestDigest(sharePointApi: string): angular.IPromise<string> {
    const deferred: angular.IDeferred<string> = this.$q.defer();

    this.$http({
      url: sharePointApi + 'contextinfo',
      method: 'POST',
      headers: {
        'Accept': 'application/json;odata=nometadata'
      }
    }).then((result: angular.IHttpPromiseCallbackArg<{ FormDigestValue: string }>): void => {
      deferred.resolve(result.data.FormDigestValue);
    }, (err: any): void => {
      deferred.reject(err);
    });

    return deferred.promise;
  }

  private getListItemEntityTypeFullName(sharePointApi: string, todoListName: string): angular.IPromise<string> {
    const deferred: angular.IDeferred<string> = this.$q.defer();

    this.$http({
      url: `${sharePointApi}web/lists/getbytitle('${todoListName}')?$select=ListItemEntityTypeFullName`,
      method: 'GET',
      headers: {
        'Accept': 'application/json;odata=nometadata'
      }
    }).then((result: angular.IHttpPromiseCallbackArg<{ ListItemEntityTypeFullName: string }>): void => {
      deferred.resolve(result.data.ListItemEntityTypeFullName);
    }, (err: any): void => {
      deferred.reject(err);
    });

    return deferred.promise;
  }
}
```

#### <a name="broadcast-properties-change-event"></a><span data-ttu-id="91c69-232">Трансляция события изменения свойств</span><span class="sxs-lookup"><span data-stu-id="91c69-232">Broadcast properties change event</span></span>

<span data-ttu-id="91c69-233">В файле **./src/webparts/toDo/ToDoWebPart.ts** добавьте к классу **ToDoWebPart** новое свойство под названием `$injector`:</span><span class="sxs-lookup"><span data-stu-id="91c69-233">In the **./src/webparts/toDo/ToDoWebPart.ts** file, to the **ToDoWebPart** class add a new property called `$injector`:</span></span>

```ts
export default class ToDoWebPart extends BaseClientSideWebPart<IToDoWebPartProps> {
  private $injector: angular.auto.IInjectorService;
  // ...
}
```

<span data-ttu-id="91c69-234">В том же файле измените метод **render** так:</span><span class="sxs-lookup"><span data-stu-id="91c69-234">In the same file, update the **render** method to:</span></span>

```ts
export default class ToDoWebPart extends BaseClientSideWebPart<IToDoWebPartProps> {
  // ...
  public render(): void {
    if (this.renderedOnce === false) {
      require('./app/app.module');

      this.domElement.innerHTML = `
        <div class="${styles.toDo}">
          <div data-ng-controller="HomeController as vm">
            <div class="${styles.configurationNeeded}" ng-show="vm.configurationNeeded">
              Please configure the web part
            </div>
            <div ng-show="vm.configurationNeeded === false">
              <div id="loading" ng-show="vm.isLoading">
                <uif-spinner>Loading...</uif-spinner>
              </div>
              <div id="entryform" ng-show="vm.isLoading === false">
                <uif-textfield uif-label="New to do:" uif-underlined ng-model="vm.newItem" ng-keydown="vm.todoKeyDown($event)"></uif-textfield>
              </div>
              <uif-list id="items" ng-show="vm.isLoading === false" >
                <uif-list-item ng-repeat="todo in vm.todoCollection" uif-item="todo" ng-class="{'${styles.done}': todo.done}">
                  <uif-list-item-primary-text>{{todo.title}}</uif-list-item-primary-text>
                  <uif-list-item-actions>
                    <uif-list-item-action ng-click="vm.completeTodo(todo)" ng-show="todo.done === false">
                      <i class="ms-Icon ms-Icon--CheckMark" aria-hidden="true"></i>
                    </uif-list-item-action>
                    <uif-list-item-action ng-click="vm.undoTodo(todo)" ng-show="todo.done">
                      <i class="ms-Icon ms-Icon--RevToggleKey" aria-hidden="true"></i>
                    </uif-list-item-action>
                    <uif-list-item-action ng-click="vm.deleteTodo(todo)">
                      <i class="ms-Icon ms-Icon--Delete" aria-hidden="true"></i>
                    </uif-list-item-action>
                  </uif-list-item-actions>
                </uif-list-item>
              </uif-list>
            </div>
          </div>
        </div>`;

      this.$injector = angular.bootstrap(this.domElement, ['todoapp']);
    }

    this.$injector.get('$rootScope').$broadcast('configurationChanged', {
      sharePointApi: this.context.pageContext.web.absoluteUrl + '/_api/',
      todoListName: this.properties.todoListName,
      hideFinishedTasks: this.properties.hideFinishedTasks
    });
  }
  // ...
}
```

<span data-ttu-id="91c69-235">В файле **./src/webparts/toDo/ToDoWebPart.module.scss** добавьте недостающие стили для класса **.configurationNeeded**:</span><span class="sxs-lookup"><span data-stu-id="91c69-235">In the **./src/webparts/toDo/ToDo.module.scss** file add the missing styles for the **.configurationNeeded** class:</span></span>

```scss
.toDo {
  /* ... */
  .configurationNeeded {
    margin: 0 auto;
    width: 100%;
    text-align: center;
  }
  /* ... */
}
```

#### <a name="subscribe-to-the-properties-changed-event"></a><span data-ttu-id="91c69-236">Подписка на событие изменения свойств</span><span class="sxs-lookup"><span data-stu-id="91c69-236">Subscribe to the properties changed event</span></span>

<span data-ttu-id="91c69-237">Откройте в редакторе кода файл **./src/webparts/toDo/app/HomeController.ts**.</span><span class="sxs-lookup"><span data-stu-id="91c69-237">In the code editor open the **./src/webparts/toDo/app/HomeController.ts** file.</span></span>

<span data-ttu-id="91c69-238">Добавьте в класс **HomeController** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="91c69-238">In the **HomeController** class add the following properties:</span></span>

```ts
export default class HomeController {
  // ...
  private sharePointApi: string = undefined;
  private todoListName: string = undefined;
  private hideFinishedTasks: boolean = false;
  private configurationNeeded: boolean = true;
  // ...
}
```

<span data-ttu-id="91c69-239">Расширьте конструктор класса **HomeController**, внедрив службу корневой области, и замените его содержимое следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="91c69-239">Extend the constructor of the **HomeController** class with injecting the root scope service and change its contents to:</span></span>

```ts
export default class HomeController {
  // ...
  public static $inject: string[] = ['DataService', '$window', '$rootScope'];

  constructor(private dataService: IDataService,
    private $window: angular.IWindowService,
    $rootScope: angular.IRootScopeService) {
    const vm: HomeController = this;
    this.init(undefined, undefined);

    $rootScope.$on('configurationChanged',
      (event: angular.IAngularEvent,
       args: {
         sharePointApi: string;
         todoListName: string;
         hideFinishedTasks: boolean;
        }): void => {
      vm.init(args.sharePointApi, args.todoListName, args.hideFinishedTasks);
    });
  }

  // ...
}
```

<span data-ttu-id="91c69-240">Добавьте в класс **HomeController** метод **init**:</span><span class="sxs-lookup"><span data-stu-id="91c69-240">To the **HomeController** class add the **init** method:</span></span>

```ts
export default class HomeController {
  // ...
  private init(sharePointApi: string, todoListName: string, hideFinishedTasks?: boolean): void {
    if (sharePointApi !== undefined && sharePointApi.length > 0 &&
      todoListName !== undefined && todoListName.length > 0) {
      this.sharePointApi = sharePointApi;
      this.todoListName = todoListName;
      this.hideFinishedTasks = hideFinishedTasks;
      this.loadTodos();
      this.configurationNeeded = false;
    }
    else {
      this.configurationNeeded = true;
    }
  }
  // ...
}
```

<span data-ttu-id="91c69-241">Обновите все остальные методы класса **HomeController**, чтобы в них использовались значения конфигурации из свойств класса:</span><span class="sxs-lookup"><span data-stu-id="91c69-241">Update all remaining methods in the **HomeController** class to use the configuration values from the class properties:</span></span>

```ts
export default class HomeController {
  // ...
  private loadTodos(): void {
    this.isLoading = true;
    this.dataService.getTodos(this.sharePointApi, this.todoListName, this.hideFinishedTasks)
      .then((todos: ITodo[]): void => {
        this.todoCollection = todos;
      })
      .finally((): void => {
        this.isLoading = false;
      });
  }

  public todoKeyDown($event: KeyboardEvent): void {
    if ($event.keyCode === 13 && this.newItem.length > 0) {
      $event.preventDefault();

      this.todoCollection.unshift({ id: -1, title: this.newItem, done: false });

      this.dataService.addTodo(this.newItem, this.sharePointApi, this.todoListName)
        .then((): void => {
          this.newItem = null;
          this.dataService.getTodos(this.sharePointApi, this.todoListName, this.hideFinishedTasks)
            .then((todos: ITodo[]): void => {
              this.todoCollection = todos;
            });
        });
    }
  }

  public deleteTodo(todo: ITodo): void {
    if (this.$window.confirm('Are you sure you want to delete this todo item?')) {
      let index: number = -1;
      for (let i: number = 0; i < this.todoCollection.length; i++) {
        if (this.todoCollection[i].id === todo.id) {
          index = i;
          break;
        }
      }

      if (index > -1) {
        this.todoCollection.splice(index, 1);
      }

      this.dataService.deleteTodo(todo, this.sharePointApi, this.todoListName)
        .then((): void => {
          this.dataService.getTodos(this.sharePointApi, this.todoListName, this.hideFinishedTasks)
            .then((todos: ITodo[]): void => {
              this.todoCollection = todos;
            });
        });
    }
  }

  public completeTodo(todo: ITodo): void {
    todo.done = true;

    this.dataService.setTodoStatus(todo, true, this.sharePointApi, this.todoListName)
      .then((): void => {
        this.dataService.getTodos(this.sharePointApi, this.todoListName, this.hideFinishedTasks)
          .then((todos: ITodo[]): void => {
            this.todoCollection = todos;
          });
      });
  }

  public undoTodo(todo: ITodo): void {
    todo.done = false;

    this.dataService.setTodoStatus(todo, false, this.sharePointApi, this.todoListName)
      .then((): void => {
        this.dataService.getTodos(this.sharePointApi, this.todoListName, this.hideFinishedTasks)
          .then((todos: ITodo[]): void => {
            this.todoCollection = todos;
          });
      });
  }
}
```

<span data-ttu-id="91c69-242">Проверьте работу веб-части, выполнив в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="91c69-242">Verify that the web part is working correctly by executing in the command line:</span></span>

```sh
gulp serve --nobrowser
```

<span data-ttu-id="91c69-243">В веб-браузере откройте рабочую область SharePoint и добавьте веб-часть на холст.</span><span class="sxs-lookup"><span data-stu-id="91c69-243">In your web browser navigate to the SharePoint workbench and add the web part to canvas. If you toggle the Hide finished tasks option you should see completed tasks being displayed or hidden accordingly.</span></span> <span data-ttu-id="91c69-244">Если переместить переключатель **Hide finished tasks** (Скрыть выполненные задачи), выполненные задачи будут показаны или скрыты.</span><span class="sxs-lookup"><span data-stu-id="91c69-244">In your web browser navigate to the SharePoint workbench and add the web part to canvas. If you toggle the **Hide finished tasks** option you should see completed tasks being displayed or hidden accordingly.</span></span>

![Приложение AngularJS со скрытыми выполненными задачами](../../../images/ng-migration-finished-tasks-hidden.png)
