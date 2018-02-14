---
title: "Руководство. Создание клиентских веб-частей SharePoint Framework с помощью AngularJS"
description: "Создание клиентской веб-части для управления элементами списков дел с использованием AngularJS и выбор ее стиля с помощью Office UI Fabric."
ms.date: 01/29/2018
ms.prod: sharepoint
ms.openlocfilehash: 2feb8705dac3223c7249acd31070ae46a11dd271
ms.sourcegitcommit: e4bf60eabffe63dc07f96824167d249c0678db82
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/30/2018
---
# <a name="build-sharepoint-framework-client-side-web-parts-with-angularjs"></a><span data-ttu-id="80a5e-103">Создание клиентских веб-частей SharePoint Framework с помощью AngularJS</span><span class="sxs-lookup"><span data-stu-id="80a5e-103">Build SharePoint Framework client-side web parts with AngularJS</span></span>

<span data-ttu-id="80a5e-104">Популярную платформу AngularJS также можно использовать для создания клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="80a5e-104">If you are familiar with AngularJS, you can also use this extremely popular framework to build client-side web parts.</span></span> <span data-ttu-id="80a5e-105">Благодаря модульности с ее помощью можно создавать что-угодно — от сложных одностраничных приложений с различными представлениями до небольших компонентов, таких как веб-части.</span><span class="sxs-lookup"><span data-stu-id="80a5e-105">Thanks to its modularity, it can be used for anything ranging from complex multi-view Single Page Applications to smaller components such as web parts.</span></span> <span data-ttu-id="80a5e-106">Раньше во многих организациях решения для SharePoint создавались с помощью AngularJS.</span><span class="sxs-lookup"><span data-stu-id="80a5e-106">Many organizations have been using AngularJS for building SharePoint solutions in the past.</span></span> <span data-ttu-id="80a5e-107">В этой статье описано, как с помощью AngularJS создать клиентскую веб-часть SharePoint Framework, а также выбрать для нее стиль, используя [Office UI Fabric](https://developer.microsoft.com/ru-RU/fabric).</span><span class="sxs-lookup"><span data-stu-id="80a5e-107">This article shows how to use AngularJS to build a SharePoint Framework client-side web part and have it styled using [Office UI Fabric](https://developer.microsoft.com/ru-RU/fabric).</span></span> 

<span data-ttu-id="80a5e-108">Работая с этим руководством, вы создадите простую веб-часть для управления элементами списка дел.</span><span class="sxs-lookup"><span data-stu-id="80a5e-108">During this tutorial you will build a simple web part that manages to do items.</span></span>

![Клиентская веб-часть SharePoint Framework, созданная на основе AngularJS, в системе разработки SharePoint](../../../images/ng-intro-hide-finished-tasks.png)

<span data-ttu-id="80a5e-110">Исходный код рабочей веб-части доступен на сайте GitHub по адресу [samples/angular-todo/](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/angular-todo).</span><span class="sxs-lookup"><span data-stu-id="80a5e-110">The source of the working web part is available on GitHub at [https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/angular-todo](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/angular-todo).</span></span>

> [!NOTE] 
> <span data-ttu-id="80a5e-111">Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки](../../set-up-your-development-environment.md) для создания решений на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="80a5e-111">Before following the steps in this article, be sure to [set up your development environment](../../set-up-your-development-environment.md) for building SharePoint Framework solutions.</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="80a5e-112">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="80a5e-112">Create a new project</span></span>

1. <span data-ttu-id="80a5e-113">Создайте папку для проекта.</span><span class="sxs-lookup"><span data-stu-id="80a5e-113">Create a new folder for your project:</span></span>

  ```sh
  md angular-todo
  ```

2. <span data-ttu-id="80a5e-114">Перейдите в папку проекта:</span><span class="sxs-lookup"><span data-stu-id="80a5e-114">Navigate to the project folder:</span></span>

  ```sh
  cd angular-todo
  ```

3. <span data-ttu-id="80a5e-115">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы выполнить скаффолдинг нового проекта на платформе SharePoint Framework:</span><span class="sxs-lookup"><span data-stu-id="80a5e-115">In the project folder, run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project:</span></span>

  ```sh
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="80a5e-116">Определите значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="80a5e-116">When prompted, define values as follows:</span></span>

  - <span data-ttu-id="80a5e-117">**angular-todo** как имя решения</span><span class="sxs-lookup"><span data-stu-id="80a5e-117">**angular-todo** as your solution name</span></span>
  - <span data-ttu-id="80a5e-118">**Use the current folder** (Использовать текущую папку) как расположение файлов</span><span class="sxs-lookup"><span data-stu-id="80a5e-118">**Use the current folder** for the location to place the files</span></span>
  - <span data-ttu-id="80a5e-119">**No JavaScript web framework** (Без веб-платформы JavaScript) как отправная точка создания веб-части</span><span class="sxs-lookup"><span data-stu-id="80a5e-119">**No JavaScript web framework** as the starting point to build the web part</span></span>
  - <span data-ttu-id="80a5e-120">**To do** (Текущие дела) как имя веб-части</span><span class="sxs-lookup"><span data-stu-id="80a5e-120">**To do** as your web part name</span></span>
  - <span data-ttu-id="80a5e-121">**Simple management of to do tasks** (Простое управление задачами) как описание веб-части</span><span class="sxs-lookup"><span data-stu-id="80a5e-121">**Simple management of to do tasks** as your web part description</span></span>

  ![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/ng-intro-yeoman-generator.png)

5. <span data-ttu-id="80a5e-123">По завершении скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="80a5e-123">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

6. <span data-ttu-id="80a5e-124">Откройте папку проекта в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="80a5e-124">Open your project folder in your code editor.</span></span> <span data-ttu-id="80a5e-125">В этом руководстве используется Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="80a5e-125">In this tutorial, you will use Visual Studio Code.</span></span>

  ![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/ng-intro-project-visual-studio-code.png)


## <a name="add-angularjs"></a><span data-ttu-id="80a5e-127">Добавление AngularJS</span><span class="sxs-lookup"><span data-stu-id="80a5e-127">Add AngularJS</span></span>

<span data-ttu-id="80a5e-128">В этом руководстве показано, как загрузить AngularJS из сети CDN.</span><span class="sxs-lookup"><span data-stu-id="80a5e-128">In this tutorial you will load AngularJS from CDN.</span></span> 

<span data-ttu-id="80a5e-129">Откройте в редакторе кода файл **config/config.json** и добавьте следующие строки в свойстве **externals**:</span><span class="sxs-lookup"><span data-stu-id="80a5e-129">In the code editor, open the **config/config.json** file, and in the **externals** property, add the following lines:</span></span>

```json
"angular": {
  "path": "https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.6.6/angular.min.js",
  "globalName": "angular"
}
```

<br/>

![AngularJS добавляется к файлу config.json](../../../images/ng-intro-angular-config.png)

## <a name="add-angularjs-typings-for-typescript"></a><span data-ttu-id="80a5e-131">Добавление определений типов AngularJS для TypeScript</span><span class="sxs-lookup"><span data-stu-id="80a5e-131">Add AngularJS typings for TypeScript</span></span>

<span data-ttu-id="80a5e-132">Так как в коде веб-части вы ссылаетесь на AngularJS, вам также нужны определения типов AngularJS для TypeScript.</span><span class="sxs-lookup"><span data-stu-id="80a5e-132">Because you are referencing AngularJS in your web part's code, you also need AngularJS typings for TypeScript.</span></span> 

<span data-ttu-id="80a5e-133">Чтобы установить их, выполните в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="80a5e-133">To install them run the following in the command line:</span></span>

```sh
npm install @types/angular --save-dev
```

## <a name="implement-angularjs-application"></a><span data-ttu-id="80a5e-134">Реализация приложения AngularJS</span><span class="sxs-lookup"><span data-stu-id="80a5e-134">Implement AngularJS application</span></span>

<span data-ttu-id="80a5e-135">Установив все необходимые компоненты, можете начинать реализацию примера приложения AngularJS.</span><span class="sxs-lookup"><span data-stu-id="80a5e-135">With all prerequisites in place you can start implementing the sample AngularJS application.</span></span> <span data-ttu-id="80a5e-136">Так как этот пример состоит из нескольких файлов, создайте для него отдельную папку **app**.</span><span class="sxs-lookup"><span data-stu-id="80a5e-136">Because it will consist of a few files, create a separate folder for it called **app**.</span></span>

![Папка app, выделенная в Visual Studio Code](../../../images/ng-intro-app-folder.png)

### <a name="implement-to-do-data-service"></a><span data-ttu-id="80a5e-138">Реализация службы данных о задачах</span><span class="sxs-lookup"><span data-stu-id="80a5e-138">Implement to do data service</span></span>

<span data-ttu-id="80a5e-139">Создайте файл **DataService.ts** в папке **app**.</span><span class="sxs-lookup"><span data-stu-id="80a5e-139">In the newly created **app** folder, create a new file called **DataService.ts**.</span></span> <span data-ttu-id="80a5e-140">В файле вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="80a5e-140">In the file paste the following code:</span></span>

```typescript
export interface ITodo {
  id: number;
  title: string;
  done: boolean;
}

export interface IDataService {
  getTodos(hideFinishedTasks: boolean): angular.IPromise<ITodo[]>;
  addTodo(todo: string): angular.IPromise<{}>;
  deleteTodo(todo: ITodo): angular.IPromise<{}>;
  setTodoStatus(todo: ITodo, done: boolean): angular.IPromise<{}>;
}

export default class DataService implements IDataService {
  public static $inject: string[] = ['$q'];

  private items: ITodo[] = [
    {
      id: 1,
      title: 'Prepare demo Web Part',
      done: true
    },
    {
      id: 2,
      title: 'Show demo',
      done: false
    },
    {
      id: 3,
      title: 'Share code',
      done: false
    }
  ];
  private nextId: number = 4;

  constructor(private $q: angular.IQService) {
  }

  public getTodos(hideFinishedTasks: boolean): angular.IPromise<ITodo[]> {
    const deferred: angular.IDeferred<ITodo[]> = this.$q.defer();

    const todos: ITodo[] = [];
    for (let i: number = 0; i < this.items.length; i++) {
      if (hideFinishedTasks && this.items[i].done) {
        continue;
      }

      todos.push(this.items[i]);
    }

    deferred.resolve(todos);

    return deferred.promise;
  }

  public addTodo(todo: string): angular.IPromise<{}> {
    const deferred: angular.IDeferred<{}> = this.$q.defer();

    this.items.push({
      id: this.nextId++,
      title: todo,
      done: false
    });

    deferred.resolve();

    return deferred.promise;
  }

  public deleteTodo(todo: ITodo): angular.IPromise<{}> {
    const deferred: angular.IDeferred<{}> = this.$q.defer();

    let pos: number = -1;
    for (let i: number = 0; i < this.items.length; i++) {
      if (this.items[i].id === todo.id) {
        pos = i;
        break;
      }
    }

    if (pos > -1) {
      this.items.splice(pos, 1);
      deferred.resolve();
    }
    else {
      deferred.reject();
    }

    return deferred.promise;
  }

  public setTodoStatus(todo: ITodo, done: boolean): angular.IPromise<{}> {
    const deferred: angular.IDeferred<{}> = this.$q.defer();

    for (let i: number = 0; i < this.items.length; i++) {
      if (this.items[i].id === todo.id) {
        this.items[i].done = done;
      }
    }

    deferred.resolve();

    return deferred.promise;
  }
}
```

<br/>

![Файл DataService.ts, открытый в Visual Studio Code](../../../images/ng-intro-dataservice.png)

<span data-ttu-id="80a5e-142">В предыдущем фрагменте кода реализуются три типа:</span><span class="sxs-lookup"><span data-stu-id="80a5e-142">In the previous code snippet, you implement three types:</span></span> 
- <span data-ttu-id="80a5e-143">интерфейс **ITodo**, который представляет элемент списка дел в приложении;</span><span class="sxs-lookup"><span data-stu-id="80a5e-143">The **ITodo** interface, which represents a To Do item in your application.</span></span>
- <span data-ttu-id="80a5e-144">интерфейс **IDataService**, который определяет подпись службы данных;</span><span class="sxs-lookup"><span data-stu-id="80a5e-144">The **IDataService** interface, which defines the signature of the data service.</span></span>
- <span data-ttu-id="80a5e-145">класс **DataService**, который отвечает за получение элементов списка дел и управление ими.</span><span class="sxs-lookup"><span data-stu-id="80a5e-145">The **DataService** class, which is responsible for retrieving and manipulating To Do items.</span></span> 

<span data-ttu-id="80a5e-146">Служба данных реализует простые методы добавления и изменения элементов списка дел.</span><span class="sxs-lookup"><span data-stu-id="80a5e-146">The data service implements simple methods for adding and modifying to do items.</span></span> <span data-ttu-id="80a5e-147">Хотя операции происходят мгновенно, для единообразия каждая функция CRUD возвращает обещание.</span><span class="sxs-lookup"><span data-stu-id="80a5e-147">Even though the operations are instantaneous, for consistency each CRUD function returns a promise.</span></span>

<span data-ttu-id="80a5e-148">В этом руководстве элементы списка дел хранятся в памяти.</span><span class="sxs-lookup"><span data-stu-id="80a5e-148">In this tutorial, To Do items are stored in memory.</span></span> <span data-ttu-id="80a5e-149">Но вы можете дополнить решение, чтобы хранить элементы в списке SharePoint, и использовать службу данных для взаимодействия с SharePoint при помощи API REST.</span><span class="sxs-lookup"><span data-stu-id="80a5e-149">In this tutorial to do items are stored in memory. You could however easily extend the solution to store items in a SharePoint List and use the data service to communicate with SharePoint using its REST API.</span></span>

### <a name="implement-the-controller"></a><span data-ttu-id="80a5e-150">Реализация контроллера</span><span class="sxs-lookup"><span data-stu-id="80a5e-150">Implement the controller</span></span>

<span data-ttu-id="80a5e-151">Далее реализуйте контроллер, который упрощает взаимодействие между представлением и службой данных.</span><span class="sxs-lookup"><span data-stu-id="80a5e-151">Next, implement the controller that will facilitate communication between the view and the data service.</span></span> 

<span data-ttu-id="80a5e-152">В папке **app** создайте файл **HomeController.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="80a5e-152">In the **app** folder create a new file named **HomeController.ts** and paste the following code:</span></span>

```typescript
import { IDataService, ITodo } from './DataService';

export default class HomeController {
  public isLoading: boolean = false;
  public newItem: string = null;
  public newToDoActive: boolean = false;
  public todoCollection: any[] = [];
  private hideFinishedTasks: boolean = false;

  public static $inject: string[] = ['DataService', '$window', '$rootScope'];

  constructor(private dataService: IDataService, private $window: angular.IWindowService, private $rootScope: angular.IRootScopeService) {
    const vm: HomeController = this;
    this.init();
  }

  private init(hideFinishedTasks?: boolean): void {
    this.hideFinishedTasks = hideFinishedTasks;
    this.loadTodos();
  }

  private loadTodos(): void {
    const vm: HomeController = this;
    this.isLoading = true;
    this.dataService.getTodos(vm.hideFinishedTasks)
      .then((todos: ITodo[]): void => {
        vm.todoCollection = todos;
      })
      .finally((): void => {
        vm.isLoading = false;
      });
  }

  public todoKeyDown($event: any): void {
    if ($event.keyCode === 13 && this.newItem.length > 0) {
      $event.preventDefault();

      this.todoCollection.unshift({ id: -1, title: this.newItem, done: false });
      const vm: HomeController = this;

      this.dataService.addTodo(this.newItem)
        .then((): void => {
          this.newItem = null;
          this.dataService.getTodos(vm.hideFinishedTasks)
            .then((todos: any[]): void => {
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

      const vm: HomeController = this;

      this.dataService.deleteTodo(todo)
        .then((): void => {
          this.dataService.getTodos(vm.hideFinishedTasks)
            .then((todos: any[]): void => {
              this.todoCollection = todos;
            });
        });
    }
  }

  public completeTodo(todo: ITodo): void {
    todo.done = true;

    const vm: HomeController = this;

    this.dataService.setTodoStatus(todo, true)
      .then((): void => {
        this.dataService.getTodos(vm.hideFinishedTasks)
          .then((todos: any[]): void => {
            this.todoCollection = todos;
          });
      });
  }

  public undoTodo(todo: ITodo): void {
    todo.done = false;

    const vm: HomeController = this;

    this.dataService.setTodoStatus(todo, false)
      .then((): void => {
        this.dataService.getTodos(vm.hideFinishedTasks)
          .then((todos: any[]): void => {
            this.todoCollection = todos;
          });
      });
  }
}
```

<br/>

![Файл HomeController.ts, открытый в Visual Studio Code](../../../images/ng-intro-homecontroller.png)

<span data-ttu-id="80a5e-154">Для начала загрузите реализованную ранее службу данных.</span><span class="sxs-lookup"><span data-stu-id="80a5e-154">You start by loading the previously implemented data service.</span></span> <span data-ttu-id="80a5e-155">Она нужна контроллеру для получения списка элементов и их изменения по запросу пользователя.</span><span class="sxs-lookup"><span data-stu-id="80a5e-155">The controller needs it in order to get the list of items and modify items as requested by the user.</span></span> <span data-ttu-id="80a5e-156">С помощью системы внедрения зависимостей AngularJS служба внедряется в контроллер.</span><span class="sxs-lookup"><span data-stu-id="80a5e-156">Using AngularJS's dependency injection the service is injected into the controller.</span></span> <span data-ttu-id="80a5e-157">Контроллер реализует ряд функций, доступных для модели представления, которые вызываются из шаблона.</span><span class="sxs-lookup"><span data-stu-id="80a5e-157">The controller implements a number of functions that are exposed to the view model and will be called from the template.</span></span> <span data-ttu-id="80a5e-158">С помощью этих функций пользователи могут добавлять и удалять задачи, а также помечать их как завершенные или незавершенные.</span><span class="sxs-lookup"><span data-stu-id="80a5e-158">Using these functions users will be able to add new items, mark items as finished, to do, or delete items.</span></span>

### <a name="implement-the-main-module"></a><span data-ttu-id="80a5e-159">Реализация основного модуля</span><span class="sxs-lookup"><span data-stu-id="80a5e-159">Implement the main module</span></span>

<span data-ttu-id="80a5e-160">Далее определите основной модуль приложения и зарегистрируйте в нем службу данных и контроллер.</span><span class="sxs-lookup"><span data-stu-id="80a5e-160">With the data service and the controller ready, define the main module of your application and register the data service and controller with it.</span></span> 

<span data-ttu-id="80a5e-161">В папке **app** создайте файл **app-module.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="80a5e-161">In the **app** folder create a new file called **app-module.ts** and paste the following contents:</span></span>

```typescript
import * as angular from 'angular';
import HomeController from './HomeController';
import DataService from './DataService';

const todoapp: angular.IModule = angular.module('todoapp', []);

todoapp
  .controller('HomeController', HomeController)
  .service('DataService', DataService);
```

<br/>

![Файл app-module.ts, открытый в Visual Studio Code](../../../images/ng-intro-app-module.png)

<span data-ttu-id="80a5e-163">Для начала добавьте ссылки на AngularJS и загрузите реализованные ранее контроллер и службу данных.</span><span class="sxs-lookup"><span data-stu-id="80a5e-163">You start by referencing AngularJS and by loading previously implemented controller and data service.</span></span> <span data-ttu-id="80a5e-164">Далее определите модуль для приложения.</span><span class="sxs-lookup"><span data-stu-id="80a5e-164">Next, you define the module for your application.</span></span> <span data-ttu-id="80a5e-165">Наконец, зарегистрируйте в приложении контроллер и службу данных.</span><span class="sxs-lookup"><span data-stu-id="80a5e-165">Finally, you register the controller and data service with your application.</span></span>

<span data-ttu-id="80a5e-166">Вы создали приложение AngularJS для веб-части.</span><span class="sxs-lookup"><span data-stu-id="80a5e-166">Now you've built an AngularJS application for your web part.</span></span> <span data-ttu-id="80a5e-167">Далее вы зарегистрируете приложение AngularJS в веб-части и сделаете его настраиваемым с помощью свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="80a5e-167">In the following steps you will register the AngularJS application with the web part and make it configurable using web part properties.</span></span>

## <a name="register-angularjs-application-with-web-part"></a><span data-ttu-id="80a5e-168">Регистрация приложения AngularJS в веб-части</span><span class="sxs-lookup"><span data-stu-id="80a5e-168">Register AngularJS application with web part</span></span>

<span data-ttu-id="80a5e-169">Следующий шаг — добавление приложения AngularJS в веб-часть.</span><span class="sxs-lookup"><span data-stu-id="80a5e-169">Next step is to add AngularJS application to the web part.</span></span> 

1. <span data-ttu-id="80a5e-170">В редакторе кода откройте файл **ToDoWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="80a5e-170">In the code editor open the **ToDoWebPart.ts** file.</span></span>

2. <span data-ttu-id="80a5e-171">Перед определением класса добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="80a5e-171">Just before the class declaration, add the following lines:</span></span>

  ```typescript
  import * as angular from 'angular';
  import './app/app-module';
  ```

  <br/>

  ![Операторы импорта в файле ToDoWebPart.ts, выделенные в Visual Studio Code](../../../images/ng-intro-web-part-import-angular.png)

  <span data-ttu-id="80a5e-173">Это позволяет загрузить ссылку на AngularJS и приложение, которые нужны для запуска приложения AngularJS.</span><span class="sxs-lookup"><span data-stu-id="80a5e-173">This allows us to load a reference to AngularJS and your application, both of which you need to bootstrap your AngularJS application.</span></span>

3. <span data-ttu-id="80a5e-174">Измените функцию **render** веб-части, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="80a5e-174">Change the web part's **render** function to:</span></span>

  ```typescript
  public render(): void {
    if (this.renderedOnce === false) {
      this.domElement.innerHTML = `
  <div class="${styles.toDo}">
    <div data-ng-controller="HomeController as vm">
      <div class="${styles.loading}" ng-show="vm.isLoading">
        <div class="${styles.spinner}">
          <div class="${styles.spinnerCircle} ${styles.spinnerLarge}"></div>
          <div class="${styles.spinnerLabel}">Loading...</div>
        </div>
      </div>
      <div ng-show="vm.isLoading === false">
        <div class="${styles.textField} ${styles.underlined}" ng-class="{'${styles.isActive}': vm.newToDoActive}">
          <label for="newToDo" class="${styles.label}">New to do:</label>
          <input type="text" label="New to do:" id="newToDo" value="" class="${styles.field}" aria-invalid="false" ng-model="vm.newItem" ng-keydown="vm.todoKeyDown($event)" ng-focus="vm.newToDoActive = true" ng-blur="vm.newToDoActive = false">
        </div>
      </div>
      <div class="list" ng-show="vm.isLoading === false">
        <div class="listSurface">
          <div class="listPage">
            <div class="listCell" ng-repeat="todo in vm.todoCollection" uif-item="todo" ng-class="{'${styles.done}': todo.done}">
              <div class="${styles.listItem}">
                <span class="${styles.listItemPrimaryText}">{{todo.title}}</span>
                <div class="${styles.listItemActions}">
                  <div class="${styles.listItemAction}" ng-click="vm.completeTodo(todo)" ng-show="todo.done === false">
                    <i class="${styles.icon} ${styles.iconCheckMark}"></i>
                  </div>
                  <div class="${styles.listItemAction}" ng-click="vm.undoTodo(todo)" ng-show="todo.done">
                    <i class="${styles.icon} ${styles.iconUndo}"></i>
                  </div>
                  <div class="${styles.listItemAction}" ng-click="vm.deleteTodo(todo)">
                    <i class="${styles.icon} ${styles.iconRecycleBin}"></i>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>`;

      angular.bootstrap(this.domElement, ['todoapp']);
    }
  }
  ```

  <br/>

  ![Функция веб-части render в Visual Studio Code](../../../images/ng-intro-web-part-render-angular.png)

4. <span data-ttu-id="80a5e-176">Код сначала присваивает шаблон приложения непосредственно элементу DOM веб-части.</span><span class="sxs-lookup"><span data-stu-id="80a5e-176">The code first assigns the template of your application directly to the web part's DOM element.</span></span> <span data-ttu-id="80a5e-177">В корневом элементе укажите имя контроллера, который обрабатывает события и привязку данных в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="80a5e-177">On the root element you specify the name of the controller that will handle events and data binding in the template.</span></span> 

5. <span data-ttu-id="80a5e-178">Запустите приложение, указав имя **todoapp**, которое вы использовали при определении основного модуля.</span><span class="sxs-lookup"><span data-stu-id="80a5e-178">Then, you bootstrap your application using the **todoapp** name you used previously when declaring the main module.</span></span> 

6. <span data-ttu-id="80a5e-179">Свойство веб-части **renderedOnce** необходимо, чтобы запуск приложения AngularJS выполнялся только один раз.</span><span class="sxs-lookup"><span data-stu-id="80a5e-179">Using the **renderedOnce** web part property you ensure that your AngularJS application is bootstrapped only once.</span></span> <span data-ttu-id="80a5e-180">Без него при изменении одного из свойств веб-части функция **render** снова запустит приложение AngularJS, что приведет к ошибке.</span><span class="sxs-lookup"><span data-stu-id="80a5e-180">Without it, if you changed one of the web part's properties, the **render** function would be invoked again bootstrapping the AngularJS application again, which would lead to an error.</span></span>

7. <span data-ttu-id="80a5e-181">Реализуйте стили CSS, которые вы используете с шаблоном.</span><span class="sxs-lookup"><span data-stu-id="80a5e-181">You also need to implement CSS styles that you are using the template.</span></span> <span data-ttu-id="80a5e-182">В редакторе кода откройте файл **ToDo.module.scss** и замените его содержимое на следующие строки:</span><span class="sxs-lookup"><span data-stu-id="80a5e-182">In the code editor open the **ToDo.module.scss** file and replace its contents with:</span></span>

  ```css
  .toDo {
    .loading {
      margin: 0 auto;
      width: 6em;

      .spinner {
        display: inline-block;
        margin: 10px 0;

        @-webkit-keyframes spinnerSpin {
          0% {
            -webkit-transform:rotate(0);
            transform:rotate(0);
          }
          100% {
            -webkit-transform:rotate(360deg);
            transform:rotate(360deg);
          }
        }
        @keyframes spinnerSpin {
          0% {
            -webkit-transform:rotate(0);
            transform:rotate(0);
          }
          100% {
            -webkit-transform:rotate(360deg);
            transform:rotate(360deg);
          }
        }

        .spinnerCircle {
          margin: auto;
          box-sizing: border-box;
          border-radius: 50%;
          width: 100%;
          height: 100%;
          border: 1.5px solid #c7e0f4;
          border-top-color: #0078d7;
          -webkit-animation: spinnerSpin 1.3s infinite cubic-bezier(.53, .21, .29, .67);
          animation: spinnerSpin 1.3s infinite cubic-bezier(.53, .21, .29, .67);

          &.spinnerLarge {
            width: 28px;
            height: 28px;
          }
        }

        .spinnerLabel {
          color: #0078d7;
          margin-top: 10px;
          text-align: center;
        }
      }
    }

    .label {
      font-family: "Segoe UI WestEuropean", "Segoe UI", -apple-system, BlinkMacSystemFont, Roboto, "Helvetica Neue", sans-serif;
      -webkit-font-smoothing: antialiased;
      font-size: 14px;
      font-weight: 400;
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      box-shadow: none;
      color: #333333;
      box-sizing: border-box;
      display: block;
      padding: 5px 0
    }

    .textField {
      font-family: "Segoe UI WestEuropean", "Segoe UI", -apple-system, BlinkMacSystemFont, Roboto, "Helvetica Neue", sans-serif;
      -webkit-font-smoothing: antialiased;
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      box-shadow: none;
      color: #333333;
      font-size: 14px;
      font-weight: 400;
      margin-bottom: 8px;

      &.underlined {
        border-bottom: 1px solid #c8c8c8;
        display: table;
        width: 100%;

        &:hover {
          border-color: #767676;
        }

        &.isActive, &:active {
          border-color: #0078d7;
        }

        .field {
          border: 0;
          display: table-cell;
          padding-top: 8px;
          padding-bottom: 3px
        }
      }

      .label {
        padding-right: 0;
        padding-left: 12px;
        margin-right: 8px;
        font-size: 14px;
        display: table-cell;
        vertical-align: top;
        padding-top: 9px;
        height: 32px;
        width: 1%;
        white-space: nowrap;
        font-weight: 400;
      }

      .field {
        text-align: left;
        float: left;
        box-sizing: border-box;
        margin: 0;
        padding: 0;
        box-shadow: none;
        font-family: "Segoe UI WestEuropean", "Segoe UI", -apple-system, BlinkMacSystemFont, Roboto, "Helvetica Neue", sans-serif;
        -webkit-font-smoothing: antialiased;
        border: 1px solid #c8c8c8;
        border-radius: 0;
        font-weight: 400;
        font-size: 14px;
        color: #333333;
        height: 32px;
        padding: 0 12px 0 12px;
        width: 100%;
        outline: 0;
        text-overflow: ellipsis;
      }

      .field:hover {
        border-color: #767676;
      }
    }

    .listItem {
      font-family: "Segoe UI WestEuropean", "Segoe UI", -apple-system, BlinkMacSystemFont, Roboto, "Helvetica Neue", sans-serif;
      -webkit-font-smoothing: antialiased;
      font-size: 14px;
      font-weight: 400;
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      box-shadow: none;
      padding: 9px 28px 3px;
      position: relative;
      display: block;

      &::before {
        display: table;
        content: "";
        line-height: 0;
      }

      &::after {
        display: table;
        content: "";
        line-height: 0;
        clear: both;
      }

      .listItemPrimaryText {
        font-family: "Segoe UI WestEuropean", "Segoe UI", -apple-system, BlinkMacSystemFont, Roboto, "Helvetica Neue", sans-serif;
        -webkit-font-smoothing: antialiased;
        font-size: 21px;
        font-weight: 100;
        padding-right: 80px;
        position: relative;
        top: -4px;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
        display: block;
      }

      .listItemActions {
        max-width: 80px;
        position: absolute;
        right: 30px;
        text-align: right;
        top: 10px;

        .listItemAction {
          color: #a6a6a6;
          display: inline-block;
          font-size: 15px;
          position: relative;
          text-align: center;
          top: 3px;
          cursor: pointer;
          height: 16px;
          width: 16px;

          &:hover {
            color: #666666;
            outline: 1px solid transparent;
          }

          .icon {
            vertical-align: top;
          }
        }
      }
    }

    .done {
      text-decoration: line-through;
    }

    .icon {
      -moz-osx-font-smoothing: grayscale;
      -webkit-font-smoothing: antialiased;
      display: inline-block;
      font-family: FabricMDL2Icons;
      font-style: normal;
      font-weight: 400;
      speak: none;

      &.iconCheckMark::before {
        content: "\E73E";
      }

      &.iconUndo::before {
        content: "\E7A7";
      }

      &.iconRecycleBin::before {
        content: "\EF87";
      }
    }
  }
  ```

  <br/>

  ![Файл ToDo.module.scss, открытый в Visual Studio Code](../../../images/ng-intro-web-part-css.png)

8. <span data-ttu-id="80a5e-184">Выполните следующую команду, чтобы убедиться, что всё работает правильно:</span><span class="sxs-lookup"><span data-stu-id="80a5e-184">Run the following command to confirm that everything is working as expected:</span></span>

  ```sh
  gulp serve
  ```

9. <span data-ttu-id="80a5e-185">В браузере должна появиться ваша веб-часть с элементами списка дел.</span><span class="sxs-lookup"><span data-stu-id="80a5e-185">In the browser you should see your To do web part showing to do items.</span></span>

  ![Веб-часть с элементами списка дел, отрисованная с помощью Office UI Fabric](../../../images/ng-intro-workbench-office-ui-fabric.png)

## <a name="make-web-part-configurable"></a><span data-ttu-id="80a5e-187">Как сделать веб-часть настраиваемой</span><span class="sxs-lookup"><span data-stu-id="80a5e-187">Make web part configurable</span></span>

<span data-ttu-id="80a5e-188">Сейчас в веб-части отображается неизменяемый список дел.</span><span class="sxs-lookup"><span data-stu-id="80a5e-188">At this point, the To Do web part shows a fixed list of To Do items.</span></span> <span data-ttu-id="80a5e-189">Далее мы дополним ее, чтобы пользователи могли решать, показывать ли задачи, помеченные как завершенные.</span><span class="sxs-lookup"><span data-stu-id="80a5e-189">At this point the To do web part shows a fixed list of to do items. Next, you will extend it with a configuration option to allow users to choose whether they want to see items that are marked as done or not.</span></span>

### <a name="add-property-in-the-web-part-manifest"></a><span data-ttu-id="80a5e-190">Добавление свойства в манифест веб-части</span><span class="sxs-lookup"><span data-stu-id="80a5e-190">Add property in the web part manifest</span></span>

<span data-ttu-id="80a5e-191">Для начала добавьте свойство настройки в манифест веб-части.</span><span class="sxs-lookup"><span data-stu-id="80a5e-191">Start by adding configuration property in the web part manifest.</span></span> 

<span data-ttu-id="80a5e-192">В редакторе кода откройте файл **ToDoWebPart.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="80a5e-192">In the code editor open the **ToDoWebPart.manifest.json** file.</span></span> <span data-ttu-id="80a5e-193">В разделе **preconfiguredEntries** перейдите к массиву **properties** и замените свойство **description** следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="80a5e-193">In the **preconfiguredEntries** section, navigate to the **properties** array and replace the existing **description** property with the following line:</span></span>

```json
"hideFinishedTasks": false
```

<br/>

![Свойство hideFinishedTasks, выделенное в манифесте веб-части](../../../images/ng-intro-manifest-property.png)

### <a name="update-the-signature-of-the-web-part-properties-interface"></a><span data-ttu-id="80a5e-195">Обновление подписи интерфейса свойств веб-части</span><span class="sxs-lookup"><span data-stu-id="80a5e-195">Update the signature of the web part properties interface</span></span>

<span data-ttu-id="80a5e-196">Далее обновите подпись интерфейса свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="80a5e-196">Next, update the signature of the web part properties interface.</span></span>

<span data-ttu-id="80a5e-197">В редакторе кода откройте файл **ToDoWebPart.ts** и обновите интерфейс `IToDoWebPartProps`, добавив следующее:</span><span class="sxs-lookup"><span data-stu-id="80a5e-197">In the code editor open the **ToDoWebPart.ts** file and update the `IToDoWebPartProps` interface to the following:</span></span>

```typescript
export interface IToDoWebPartProps {
  hideFinishedTasks: boolean;
}
```

<br/>

![Файл IToDoWebPartProps.ts, открытый в Visual Studio Code](../../../images/ng-intro-property-interface.png)

### <a name="add-the-property-to-the-web-part-property-pane"></a><span data-ttu-id="80a5e-199">Добавление свойства в панель свойств веб-части</span><span class="sxs-lookup"><span data-stu-id="80a5e-199">Add the property to the web part property pane</span></span>

<span data-ttu-id="80a5e-200">Чтобы пользователи могли настраивать значение нового свойства, оно должно быть доступно на панели свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="80a5e-200">To allow users to configure the value of your newly added property, you have to expose it through the web part property pane.</span></span>

1. <span data-ttu-id="80a5e-201">В редакторе кода откройте файл **ToDoWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="80a5e-201">In the code editor open the **ToDoWebPart.ts** file.</span></span> 

2. <span data-ttu-id="80a5e-202">В первом операторе `import` замените строку `PropertyPaneTextField` на строку `PropertyPaneToggle`:</span><span class="sxs-lookup"><span data-stu-id="80a5e-202">In the first `import` statement replace  `PropertyPaneTextField` with `PropertyPaneToggle`:</span></span>

  ```typescript
  import {
    BaseClientSideWebPart,
    IPropertyPaneConfiguration,
    PropertyPaneToggle
  } from '@microsoft/sp-webpart-base';
  ```

  <br/>

  ![Оператор импорта PropertyPaneToggle, выделенный в Visual Studio Code](../../../images/ng-intro-property-pane-toggle.png)

3. <span data-ttu-id="80a5e-204">Измените функцию `propertyPaneSettings`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="80a5e-204">Change the implementation of the `propertyPaneSettings` function to:</span></span>

  ```typescript
  protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
    return {
      pages: [
        {
          header: {
            description: strings.PropertyPaneDescription
          },
          groups: [
            {
              groupName: strings.ViewGroupName,
              groupFields: [
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
  ```

4. <span data-ttu-id="80a5e-205">Чтобы исправить ссылки на отсутствующие строки, сначала нужно изменить подпись строк.</span><span class="sxs-lookup"><span data-stu-id="80a5e-205">To fix the missing string references you first need to change the signature of your strings.</span></span> <span data-ttu-id="80a5e-206">В редакторе кода откройте файл **loc/mystrings.d.ts** и замените его содержимое на следующие строки:</span><span class="sxs-lookup"><span data-stu-id="80a5e-206">In the code editor open the **loc/mystrings.d.ts** file and change its contents to:</span></span>

  ```typescript
  declare interface IToDoWebPartStrings {
    PropertyPaneDescription: string;
    BasicGroupName: string;
    HideFinishedTasksFieldLabel: string;
  }

  declare module 'ToDoWebPartStrings' {
    const strings: IToDoWebPartStrings;
    export = strings;
  }
  ```

  <br/>

  ![Файл loc/mystrings.d.ts, открытый в Visual Studio Code](../../../images/ng-intro-strings-interface.png)

5. <span data-ttu-id="80a5e-208">Укажите действительные значения для новых строк.</span><span class="sxs-lookup"><span data-stu-id="80a5e-208">Next, you need to provide the actual values for the newly defined strings.</span></span> <span data-ttu-id="80a5e-209">В редакторе кода откройте файл **loc/en-us.js** и замените его содержимое на следующие строки:</span><span class="sxs-lookup"><span data-stu-id="80a5e-209">In the code editor open the **loc/en-us.js** file and change its contents to:</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Manage configuration of the To do web part",
      "ViewGroupName": "View",
      "HideFinishedTasksFieldLabel": "Hide finished tasks"
    }
  });
  ```

  <br/>

  ![Файл loc/en-us.js, открытый в Visual Studio Code](../../../images/ng-intro-strings.png)

6. <span data-ttu-id="80a5e-211">Выполните следующую команду, чтобы убедиться, что всё работает правильно:</span><span class="sxs-lookup"><span data-stu-id="80a5e-211">Run the following command to confirm that everything is working as expected:</span></span>

  ```sh
  gulp serve
  ```

7. <span data-ttu-id="80a5e-212">На панели свойств веб-части должен появиться выключатель для нового свойства.</span><span class="sxs-lookup"><span data-stu-id="80a5e-212">In the web part property pane you should see a toggle button for your newly defined property.</span></span>

  ![Выключатель в области свойств веб-части](../../../images/ng-intro-property-pane-toggle-browser.png)

  <span data-ttu-id="80a5e-214">Сейчас выключатель не работает, так как он еще не подключен к AngularJS.</span><span class="sxs-lookup"><span data-stu-id="80a5e-214">At this point clicking the toggle button doesn't have any effect on your web part as it hasn't been connected to AngularJS.</span></span> <span data-ttu-id="80a5e-215">Как это сделать, описано ниже.</span><span class="sxs-lookup"><span data-stu-id="80a5e-215">You will do that in the next step.</span></span>

### <a name="make-the-angularjs-application-configurable-using-web-part-properties"></a><span data-ttu-id="80a5e-216">Как сделать приложение AngularJS настраиваемым с помощью свойств веб-части</span><span class="sxs-lookup"><span data-stu-id="80a5e-216">Make the AngularJS application configurable using web part properties</span></span>

<span data-ttu-id="80a5e-217">Выполняя предыдущий шаг, вы определили свойство веб-части, которое позволяет пользователям решать, нужно ли показывать завершенные задачи.</span><span class="sxs-lookup"><span data-stu-id="80a5e-217">In the previous step you defined a web part property that allows users to choose whether to show completed tasks or not.</span></span> <span data-ttu-id="80a5e-218">Далее необходимо передать выбранное пользователем значение в приложение AngularJS, чтобы оно могло загрузить соответствующие элементы.</span><span class="sxs-lookup"><span data-stu-id="80a5e-218">Next you will pass the value selected by the user into the AngularJS application so that it can load items accordingly.</span></span>

#### <a name="broadcast-angularjs-event-on-web-part-property-change"></a><span data-ttu-id="80a5e-219">Трансляция события AngularJS при изменении свойства веб-части</span><span class="sxs-lookup"><span data-stu-id="80a5e-219">Broadcast AngularJS event on web part property change</span></span>

1. <span data-ttu-id="80a5e-220">В редакторе кода откройте файл **ToDoWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="80a5e-220">In the code editor open the **ToDoWebPart.ts** file.</span></span> <span data-ttu-id="80a5e-221">Добавьте следующую строку перед конструктором веб-части:</span><span class="sxs-lookup"><span data-stu-id="80a5e-221">Right before web part's constructor add the following line:</span></span>

  ```typescript
  private $injector: angular.auto.IInjectorService;
  ```

  <br/>

  ![Переменная класса $injector, выделенная в Visual Studio Code](../../../images/ng-intro-injector-class-variable.png)

2. <span data-ttu-id="80a5e-223">Измените функцию **render** веб-части, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="80a5e-223">Next, change the web part's **render** function to the following:</span></span>

  ```typescript
  public render(): void {
    if (this.renderedOnce === false) {
      this.domElement.innerHTML = `
  <div class="${styles.toDo}">
    <div data-ng-controller="HomeController as vm">
      <div class="${styles.loading}" ng-show="vm.isLoading">
        <div class="${styles.spinner}">
          <div class="${styles.spinnerCircle} ${styles.spinnerLarge}"></div>
          <div class="${styles.spinnerLabel}">Loading...</div>
        </div>
      </div>
      <div ng-show="vm.isLoading === false">
        <div class="${styles.textField} ${styles.underlined}" ng-class="{'${styles.isActive}': vm.newToDoActive}">
          <label for="newToDo" class="${styles.label}">New to do:</label>
          <input type="text" label="New to do:" id="newToDo" value="" class="${styles.field}" aria-invalid="false" ng-model="vm.newItem" ng-keydown="vm.todoKeyDown($event)" ng-focus="vm.newToDoActive = true" ng-blur="vm.newToDoActive = false">
        </div>
      </div>
      <div class="list" ng-show="vm.isLoading === false">
        <div class="listSurface">
          <div class="listPage">
            <div class="listCell" ng-repeat="todo in vm.todoCollection" uif-item="todo" ng-class="{'${styles.done}': todo.done}">
              <div class="${styles.listItem}">
                <span class="${styles.listItemPrimaryText}">{{todo.title}}</span>
                <div class="${styles.listItemActions}">
                  <div class="${styles.listItemAction}" ng-click="vm.completeTodo(todo)" ng-show="todo.done === false">
                    <i class="${styles.icon} ${styles.iconCheckMark}"></i>
                  </div>
                  <div class="${styles.listItemAction}" ng-click="vm.undoTodo(todo)" ng-show="todo.done">
                    <i class="${styles.icon} ${styles.iconUndo}"></i>
                  </div>
                  <div class="${styles.listItemAction}" ng-click="vm.deleteTodo(todo)">
                    <i class="${styles.icon} ${styles.iconRecycleBin}"></i>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>`;

      this.$injector = angular.bootstrap(this.domElement, ['todoapp']);
    }

    this.$injector.get('$rootScope').$broadcast('configurationChanged', {
      hideFinishedTasks: this.properties.hideFinishedTasks
    });
  }
  ```

<span data-ttu-id="80a5e-224">Предыдущий пример кода при каждом изменении свойства веб-части транслирует событие AngularJS, на которое его подписывает приложение AngularJS.</span><span class="sxs-lookup"><span data-stu-id="80a5e-224">In the above code sample, every time the web part property is changed, it will broadcast an AngularJS event to which the AngularJS application will subscribe it.</span></span> <span data-ttu-id="80a5e-225">Когда приложение AngularJS получит событие, оно обработает его соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="80a5e-225">When event is received by the AngularJS application, it will then handle that accordingly.</span></span>

#### <a name="subscribe-to-web-part-property-change-event-in-angularjs"></a><span data-ttu-id="80a5e-226">Подписка на событие изменения свойства веб-части в AngularJS</span><span class="sxs-lookup"><span data-stu-id="80a5e-226">Subscribe to web part property change event in AngularJS</span></span>

1. <span data-ttu-id="80a5e-227">В редакторе кода откройте файл **app/HomeController.ts**.</span><span class="sxs-lookup"><span data-stu-id="80a5e-227">In the code editor open the **app/HomeController.ts** file.</span></span> <span data-ttu-id="80a5e-228">Дополните конструктор следующим образом:</span><span class="sxs-lookup"><span data-stu-id="80a5e-228">Extend the constructor as follows:</span></span>

  ```typescript
  constructor(private dataService: IDataService, private $window: angular.IWindowService, private $rootScope: angular.IRootScopeService) {
    const vm: HomeController = this;
    this.init();

    $rootScope.$on('configurationChanged', (event: angular.IAngularEvent, args: { hideFinishedTasks: boolean }): void => {
      vm.init(args.hideFinishedTasks);
    });
  }
  ```

  <br/>

  ![Определение конструктора в файле HomeController.ts, выделенное в Visual Studio Code](../../../images/ng-intro-homecontroller-event.png)

2. <span data-ttu-id="80a5e-230">Убедитесь, что приложение AngularJS работает без ошибок и правильно отвечает на изменение свойства. Для этого в командной строке выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="80a5e-230">Verify that the AngularJS application is working as expected and correctly responding to the changed property by running the following in the command line:</span></span>

  ```sh
  gulp serve
  ```

3. <span data-ttu-id="80a5e-231">Когда вы переключите значение свойства **Скрыть завершенные задачи**, веб-часть должна показать или скрыть завершенные задачи.</span><span class="sxs-lookup"><span data-stu-id="80a5e-231">If you toggle the value of the **Hide finished tasks** property, web part should show or hide finished tasks accordingly.</span></span>

  ![В веб-части показаны только незавершенные задачи: параметр "Скрыть завершенные задачи" включен](../../../images/ng-intro-hide-finished-tasks.png)


## <a name="see-also"></a><span data-ttu-id="80a5e-233">См. также</span><span class="sxs-lookup"><span data-stu-id="80a5e-233">See also</span></span>

- [<span data-ttu-id="80a5e-234">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="80a5e-234">SharePoint Framework Extensions Overview</span></span>](../../sharepoint-framework-overview.md)
