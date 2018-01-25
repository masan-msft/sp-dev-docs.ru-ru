---
title: "Учебник: перенос пункта меню Edit Control Block (ECB) в расширения SharePoint Framework"
description: "Переход от старых (\"классических\") модификаций к новой модели на основе расширений SharePoint Framework."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: 6c790e47b826193029395ef9ca27a8abe2f6b9ca
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2018
---
# <a name="migrating-from-edit-control-block-ecb-menu-item-to-sharepoint-framework-extensions"></a><span data-ttu-id="c071b-103">Перенос пункта меню Edit Control Block (ECB) в расширения SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="c071b-103">Migrating from Edit Control Block (ECB) menu item to SharePoint Framework Extensions</span></span>

<span data-ttu-id="c071b-104">За последние несколько лет в большинстве корпоративных решений на основе Office 365 и SharePoint Online для расширения пользовательского интерфейса страниц использовалась возможность _CustomAction_ для сайтов на платформе функций SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c071b-104">During the last few years, most of the enterprise solutions built on top of Office 365 and SharePoint Online leveraged the site _CustomAction_ capability of the SharePoint Feature Framework to extend the UI of pages.</span></span> <span data-ttu-id="c071b-105">Однако в "современном" интерфейсе SharePoint Online большинство таких модификаций стало недоступным.</span><span class="sxs-lookup"><span data-stu-id="c071b-105">However nowdays, within the new "modern" UI of SharePoint Online, most of those customizations are no more available.</span></span> <span data-ttu-id="c071b-106">Реализовать схожие функции в "современном" интерфейсе можно с помощью новых расширений SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="c071b-106">Luckily, with the new SharePoint Framework Extensions you can provide similar functionality in the "modern" UI.</span></span> 

<span data-ttu-id="c071b-107">Из данного руководства вы узнаете, как перейти от старых ("классических") модификаций к новой модели на основе расширений SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="c071b-107">In this tutorial you will learn how to migrate from old "classic" customizations to the new model based on SharePoint Framework Extensions.</span></span>

> [!NOTE]
> <span data-ttu-id="c071b-108">Дополнительные сведения о создании расширений SharePoint Framework см. в статье [Обзор расширений SharePoint Framework](../overview-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="c071b-108">For more information about how to build SharePoint Framework Extensions, see [Overview of SharePoint Framework Extensions](../overview-extensions.md).</span></span>

<span data-ttu-id="c071b-109">Сначала рассмотрим доступные разработчикам варианты для создания расширений SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="c071b-109">First of all, let's introduce the available options when developing SharePoint Framework Extensions:</span></span>

* <span data-ttu-id="c071b-110">**Настройщик приложений**.</span><span class="sxs-lookup"><span data-stu-id="c071b-110">Application customizer</span></span> <span data-ttu-id="c071b-111">Расширьте встроенный "современный" пользовательский интерфейс SharePoint Online, добавив собственные элементы HTML и клиентский код к стандартным заполнителям "современных" страниц.</span><span class="sxs-lookup"><span data-stu-id="c071b-111">Application Customizer: extend the native "modern" UI of SharePoint Online by adding custom HTML elements and client-side code to pre-defined placeholders of "modern" pages.</span></span> <span data-ttu-id="c071b-112">На момент написания этой статьи заполнители доступны в верхнем и нижнем колонтитулах каждой "современной" страницы.</span><span class="sxs-lookup"><span data-stu-id="c071b-112">At the time of this writing, the available placeholders are the header and the footer of every "modern" page.</span></span>
* <span data-ttu-id="c071b-113">**Набор команд**.</span><span class="sxs-lookup"><span data-stu-id="c071b-113">Command set</span></span> <span data-ttu-id="c071b-114">Добавьте собственные элементы меню ECB или кнопки на панель команд списка или библиотеки.</span><span class="sxs-lookup"><span data-stu-id="c071b-114">Command Set: allow to add custom ECB menu items or custom buttons to the command bar of a list view for a list or a library.</span></span> <span data-ttu-id="c071b-115">С этими командами можно связать любое действие JavaScript (TypeScript).</span><span class="sxs-lookup"><span data-stu-id="c071b-115">You can associate any JavaScript (TypeScript) action to these commands.</span></span>
* <span data-ttu-id="c071b-116">**Настройщик полей**.</span><span class="sxs-lookup"><span data-stu-id="c071b-116">Field Customizer</span></span> <span data-ttu-id="c071b-117">Настройте отображение поля в списке, используя собственные элементы HTML и клиентский код.</span><span class="sxs-lookup"><span data-stu-id="c071b-117">Field Customizer: customize the rendering of a field in a list view using custom HTML elements and client-side code.</span></span>

<span data-ttu-id="c071b-118">Наиболее полезное в нашем контексте расширение — набор команд.</span><span class="sxs-lookup"><span data-stu-id="c071b-118">The most useful option in our context is the Command Set extension.</span></span>

<span data-ttu-id="c071b-119">Предположим, у вас есть элемент _CustomAction_ в SharePoint Online, необходимый для создания пункта меню ECB для документов в библиотеке.</span><span class="sxs-lookup"><span data-stu-id="c071b-119"> Assume that you have a _CustomAction_ in SharePoint Online, in order to have a custom ECB menu item for documents in a library.</span></span> <span data-ttu-id="c071b-120">Назначение пункта меню ECB — открытие настраиваемой страницы с предоставлением идентификаторов списка и выбранного в текущий момент пункта в строке запроса целевой страницы.</span><span class="sxs-lookup"><span data-stu-id="c071b-120">The scope of the ECB menu item is to open a custom page, providing the list ID and the list item ID of the currently selected item in the querystring of the target page.</span></span>

<span data-ttu-id="c071b-121">Ниже представлен XML-код этого элемента _CustomAction_ на платформе SharePoint Feature Framework.</span><span class="sxs-lookup"><span data-stu-id="c071b-121">In the following code snippet you can see the XML code defining that _CustomAction_ using the SharePoint Feature Framework.</span></span>

```XML
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <CustomAction Id="OpenDetailsPageWithItemReference"
                Title="Show Details"
                Description="Opens a new page with further details about the currently selected item"
                Sequence="1001"
                RegistrationType="List"
                RegistrationId="101"                
                Location="EditControlBlock">
    <UrlAction Url="ShowDetails.aspx?ID={ItemId}&amp;List={ListId}" />
  </CustomAction>
</Elements>
```

<span data-ttu-id="c071b-122">Как видите, в файле элементов функции определяется элемент типа _CustomAction_, чтобы добавлять новый пункт в расположении _EditControlBlock_ (ECB) для любого документа в любой библиотеке (для параметра _RegistrationType_ задано значение _List_, а для параметра _RegistrationId_ — значение _101_).</span><span class="sxs-lookup"><span data-stu-id="c071b-122">As you can see, the feature elements file defines an element of type _CustomAction_ to add a new item in the _EditControlBlock_ location (i.e. ECB) for any document in any library (_RegistrationType_ is _List_ and _RegistrationId_ is _101_).</span></span>

<span data-ttu-id="c071b-123">На приведенном ниже рисунке представлены выходные данные вышеописанного дополнительного действия в представлении списка для библиотеки.</span><span class="sxs-lookup"><span data-stu-id="c071b-123">In the following figure you can see the output of the previous custom action, within the list view of a library.</span></span>

![Пользовательский нижний колонтитул на классической странице](../../../images/ecb-menu-classic-output.png)

<span data-ttu-id="c071b-125">Обратите внимание на то, что настраиваемый элемент ECB в SharePoint Feature Framework работает и в "современном" списке.</span><span class="sxs-lookup"><span data-stu-id="c071b-125">Notice that the SharePoint Feature Framework ECB custom item works in a "modern" list, too.</span></span> <span data-ttu-id="c071b-126">Если не использовать код JavaScript, то дополнительное действие для списков будет работать и в "современных" списках.</span><span class="sxs-lookup"><span data-stu-id="c071b-126">In fact, as long as you don't use JavaScript code, a list custom action still works in "modern" lists, too.</span></span>

<span data-ttu-id="c071b-127">Ниже описано, как перенести старое решение в SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="c071b-127">To migrate the previous solution to the SharePoint Framework, see the following steps.</span></span>

> [!NOTE]
> <span data-ttu-id="c071b-128">Прежде чем выполнять действия, описанные в этой статье, обязательно [настройте среду разработки](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="c071b-128">Before following the steps in this article, be sure to [Set up your development environment](../../set-up-your-development-environment.md).</span></span>

<span data-ttu-id="c071b-129"><a name="CreateCommandSet"> </a></span><span class="sxs-lookup"><span data-stu-id="c071b-129"></span></span>

## <a name="create-a-new-sharepoint-framework-solution"></a><span data-ttu-id="c071b-130">Создание решения SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="c071b-130">Create a new SharePoint Framework solution</span></span>

1. <span data-ttu-id="c071b-131">Откройте любую командную строку (например, PowerShell, CMD.EXE или Cmder).</span><span class="sxs-lookup"><span data-stu-id="c071b-131">Open the command-line tool of your choice (for example, PowerShell, CMD.EXE, Cmder).</span></span> <span data-ttu-id="c071b-132">Создайте папку для решения под названием **spfx-ecb-extension**, а затем решение SharePoint Framework, запустив генератор Yeoman с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="c071b-132">Open the command line tool of your choice (PowerShell, CMD.EXE, Cmder, etc.), create a new folder for the solution (call it **spfx-custom-field-extension**), and create a new SharePoint Framework solution by running the Yeoman generator with the following command:</span></span>

2. <span data-ttu-id="c071b-133">При появлении соответствующих запросов укажите следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="c071b-133">When prompted by the tool, provide the following answers:</span></span>

  * <span data-ttu-id="c071b-134">Оставьте имя решения по умолчанию (**spfx-ecb-extension**) и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="c071b-134">Accept the default name (**spfx-custom-field-extension**) for your solution, and press Enter.</span></span>
  * <span data-ttu-id="c071b-135">Выберите **SharePoint Online only (latest)** (Только SharePoint Online, последняя версия) и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="c071b-135">Select **SharePoint Online only (latest)**, and select Enter.</span></span>
  * <span data-ttu-id="c071b-136">Выберите **Use the current folder** (Использовать текущую папку) и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="c071b-136">Select **Use the current folder**, and select Enter.</span></span>
  * <span data-ttu-id="c071b-137">Выберите **N**, чтобы сделать установку расширения, выполняемую напрямую, обязательной на каждом сайте при его использовании.</span><span class="sxs-lookup"><span data-stu-id="c071b-137">Select **N** to require the extension to be installed on each site explicitly when it's being used.</span></span>
  * <span data-ttu-id="c071b-138">Выберите **Extension** (Расширение) в качестве типа создаваемого клиентского компонента.</span><span class="sxs-lookup"><span data-stu-id="c071b-138">Select **Extension** as the client-side component type to be created.</span></span>
  * <span data-ttu-id="c071b-139">Выберите для создаваемого расширения тип **ListView Command Set**.</span><span class="sxs-lookup"><span data-stu-id="c071b-139">Select **ListView Command Set** as the extension type to be created.</span></span>
  * <span data-ttu-id="c071b-140">Укажите имя **CustomECB** для набора команд.</span><span class="sxs-lookup"><span data-stu-id="c071b-140">Provide "CustomECB" as the name for your Command Set.</span></span>

  ![Пользовательский интерфейс генератора Yeoman при создании решения для пользовательского нижнего колонтитула](../../../images/spfx-ecb-extension-yeoman.png)

  <span data-ttu-id="c071b-142">На этом этапе Yeoman устанавливает необходимые зависимости и выполняет скаффолдинг файлов и папок решения вместе с расширением **CustomFooter**.</span><span class="sxs-lookup"><span data-stu-id="c071b-142">At this point, Yeoman will install the required dependencies and scaffold the solution files and folders along with the **CustomFooter** extension.</span></span> <span data-ttu-id="c071b-143">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="c071b-143">This might take a few minutes.</span></span>

  <span data-ttu-id="c071b-144">После успешного формирования шаблона должно появиться следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="c071b-144">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

  ![Формирование шаблона завершено](../../../images/spfx-ecb-extension-yeoman-completed.png)

3. <span data-ttu-id="c071b-146">Чтобы заблокировать версию зависимостей проекта, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c071b-146">To lock down the version of the project dependencies, run the following command:</span></span>

  ```
  npm shrinkwrap
  ```

4. <span data-ttu-id="c071b-147">Запустите Visual Studio Code (или другой редактор кода) и начните разработку решения.</span><span class="sxs-lookup"><span data-stu-id="c071b-147">Now start Visual Studio Code (or whatever else is the code editor of your choice) and start developing the solution.</span></span> <span data-ttu-id="c071b-148">Чтобы запустить Visual Studio Code, можно выполнить приведенный ниже оператор.</span><span class="sxs-lookup"><span data-stu-id="c071b-148">To start Visual Studio Code, you can execute the following statement.</span></span>

  ```
  code .
  ```

<span data-ttu-id="c071b-149"><a name="DefineCommandSetECB"> </a></span><span class="sxs-lookup"><span data-stu-id="c071b-149"></span></span>

## <a name="define-the-new-ecb-item"></a><span data-ttu-id="c071b-150">Определение нового элемента ECB</span><span class="sxs-lookup"><span data-stu-id="c071b-150">Define the new ECB item</span></span>

<span data-ttu-id="c071b-151">Чтобы воспроизвести такое поведение пункта меню ECB, созданного с помощью SharePoint Feature Framework, нужно реализовать такую же логику с помощью клиентского кода в новом решении SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="c071b-151"> In order to reproduce the same behavior of the ECB menu item built using the SharePoint Feature Framework, you simply need to implement the same logic using client-side code, within the new SharePoint Framework solution.</span></span> <span data-ttu-id="c071b-152">Чтобы выполнить эту задачу, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c071b-152">To accomplish this task, complete the following steps.</span></span>

1. <span data-ttu-id="c071b-153">Откройте файл **CustomEcbCommandSet.manifest.json** в папке **src/extensions/customEcb**.</span><span class="sxs-lookup"><span data-stu-id="c071b-153">Open the **CustomEcbCommandSet.manifest.json** file in the **src/extensions/customEcb** folder.</span></span> <span data-ttu-id="c071b-154">Скопируйте значение свойства `id` и сохраните его в надежном месте, так как оно понадобится вам позже.</span><span class="sxs-lookup"><span data-stu-id="c071b-154">Copy the value of the `id` property and store it in a safe place, because you will need it later.</span></span>

2. <span data-ttu-id="c071b-155">В том же файле измените массив **items** в нижней части файла, чтобы определить одну команду для набора команд.</span><span class="sxs-lookup"><span data-stu-id="c071b-155">Within the same file edit the array of **"items"** in the lower part of the file, in order to define a single command for the Command Set.</span></span> <span data-ttu-id="c071b-156">Вызовите команду **ShowDetails**, а затем укажите название и тип команды.</span><span class="sxs-lookup"><span data-stu-id="c071b-156">Call the command **ShowDetails**, and then provide a title and a command type.</span></span> <span data-ttu-id="c071b-157">На приведенном ниже снимке экрана показано, как должен выглядеть файл манифеста.</span><span class="sxs-lookup"><span data-stu-id="c071b-157">In the following screenshot you can see how the manifest file should look like.</span></span>

  ![Файл манифеста для настраиваемого набора команд](../../../images/spfx-ecb-extension-manifest.png)

3. <span data-ttu-id="c071b-159">Откройте файл **CustomEcbCommandSet.ts** в папке **src/расширения/customEcb** и измените его содержимое в соответствии со следующим фрагментом кода:</span><span class="sxs-lookup"><span data-stu-id="c071b-159">Open the **CustomEcbCommandSet.ts** file in the **src/extensions/customEcb** folder and edit the content according to the following code snippet:</span></span>

  ``` TypeScript
  import { Guid } from '@microsoft/sp-core-library';
  import { override } from '@microsoft/decorators';
  import {
    BaseListViewCommandSet,
    Command,
    IListViewCommandSetListViewUpdatedParameters,
    IListViewCommandSetExecuteEventParameters
  } from '@microsoft/sp-listview-extensibility';
  import { Dialog } from '@microsoft/sp-dialog';

  import * as strings from 'CustomEcbCommandSetStrings';

  export interface ICustomEcbCommandSetProperties {
    targetUrl: string;
  }

  export default class CustomEcbCommandSet extends BaseListViewCommandSet<ICustomEcbCommandSetProperties> {

    @override
    public onInit(): Promise<void> {
      return Promise.resolve();
    }

    @override
    public onListViewUpdated(event: IListViewCommandSetListViewUpdatedParameters): void {
      const compareOneCommand: Command = this.tryGetCommand('ShowDetails');
      if (compareOneCommand) {
        // This command should be hidden unless exactly one row is selected.
        compareOneCommand.visible = event.selectedRows.length === 1;
      }
    }

    @override
    public onExecute(event: IListViewCommandSetExecuteEventParameters): void {
      switch (event.itemId) {
        case 'ShowDetails':

          const itemId: number = event.selectedRows[0].getValueByName("ID");
          const listId: Guid = this.context.pageContext.list.id;

          window.location.replace(`${this.properties.targetUrl}?ID=${itemId}&List=${listId}`);

          break;
        default:
          throw new Error('Unknown command');
      }
    }
  }
  ```

  <span data-ttu-id="c071b-160">Обратите внимание на оператор `import` в самом начале файла. Он ссылается на тип `Guid`, который будет использоваться для хранения идентификатора текущего списка.</span><span class="sxs-lookup"><span data-stu-id="c071b-160">Notice the `import` statement at the very beginning of the file, in order to reference the `Guid` type, which will be used to hold the ID of the current list.</span></span> 
  
  <span data-ttu-id="c071b-161">Более того, в интерфейсе `ICustomEcbCommandSetProperties` объявляется одно свойство с именем `targetUrl`, с помощью которого можно предоставить URL-адрес целевой страницы, открываемой при выборе пункта меню ECB.</span><span class="sxs-lookup"><span data-stu-id="c071b-161">Moreover, the interface `ICustomEcbCommandSetProperties` declares a single property called `targetUrl` that can be used to provide the URL of the target page to open when clicking on the ECB menu item.</span></span>

  <span data-ttu-id="c071b-162">Переопределенный метод `onExecute` выполняет дополнительное действие.</span><span class="sxs-lookup"><span data-stu-id="c071b-162">Furthermore, the override of the `onExecute` method handles the execution of the custom action.</span></span> <span data-ttu-id="c071b-163">Обратите внимание на фрагмент кода, считывающий идентификатор выбранного элемента из аргумента `event`, а также идентификатор исходного списка из объекта `pageContext`.</span><span class="sxs-lookup"><span data-stu-id="c071b-163">Notice the code excerpt that reads the ID of the currently selected item, from the `event` argument, and the ID of the source list from the the `pageContext` object.</span></span>

  <span data-ttu-id="c071b-164">Наконец, обратите внимание на переопределение метода `onListViewUpdated`, который по умолчанию включал команду `'ShowDetails'`, только если выбран один элемент.</span><span class="sxs-lookup"><span data-stu-id="c071b-164">Lastly, notice the override of the `onListViewUpdated` method, which by default enabled the `'ShowDetails'` command only if a single item is selected.</span></span>

  <span data-ttu-id="c071b-165">Перенаправление на целевой URL-адрес выполняется с помощью классического кода JavaScript и функции `window.location.replace`.</span><span class="sxs-lookup"><span data-stu-id="c071b-165">The redirection to the target URL is handled by using classic JavaScript code and using the `window.location.replace` function.</span></span> <span data-ttu-id="c071b-166">Конечно, вы можете написать любой код TypeScript в методе `onExecute`.</span><span class="sxs-lookup"><span data-stu-id="c071b-166">Of course, you can write whatever kind of TypeScript code you like inside the `onExecute` method.</span></span> <span data-ttu-id="c071b-167">В качестве примера можно использовать платформу диалоговых окон SharePoint Framework, чтобы открыть новое диалоговое окно и взаимодействовать с пользователями.</span><span class="sxs-lookup"><span data-stu-id="c071b-167">Just for the sake of making an example, you can leverage the SharePoint Framework Dialog Framework to open a new dialog window and to interact with the end users.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c071b-168">Дополнительные сведения о платформе SharePoint Framework см. в документе [Использование настраиваемых диалоговых окон с расширениями SharePoint Framework](./using-custom-dialogs-with-spfx.md).</span><span class="sxs-lookup"><span data-stu-id="c071b-168">For further details about the SharePoint Framework Dialog Framework you can read the document [Use custom dialog boxes with SharePoint Framework Extensions](./using-custom-dialogs-with-spfx.md).</span></span>

  <br/>

  <span data-ttu-id="c071b-169">На приведенном ниже рисунке показаны выходные данные.</span><span class="sxs-lookup"><span data-stu-id="c071b-169">In the following figure you can see the resulting output.</span></span>

  ![Набор команд ECB в "современном" списке](../../../images/spfx-ecb-extension-output.png)

<span data-ttu-id="c071b-171"><a name="DebugCommandSet"> </a></span><span class="sxs-lookup"><span data-stu-id="c071b-171"></span></span>

## <a name="test-the-solution-in-debug-mode"></a><span data-ttu-id="c071b-172">Тестирование решения в режиме отладки</span><span class="sxs-lookup"><span data-stu-id="c071b-172">Test the solution in debug mode</span></span>

1. <span data-ttu-id="c071b-173">Вернитесь в окно консоли и выполните приведенную ниже команду, чтобы выполнить сборку и запустить локальный сервер Node.js для размещения решения.</span><span class="sxs-lookup"><span data-stu-id="c071b-173">Go back to the console window and run the following command to build the solution and run the local Node.js server to host it.</span></span>

  ```
  gulp serve --nobrowser
  ```

2. <span data-ttu-id="c071b-174">Теперь откройте любой браузер и перейдите к "современной" библиотеке на любом "современном" сайте группы.</span><span class="sxs-lookup"><span data-stu-id="c071b-174">Now open your favorite browser and go to a "modern" library of any "modern" team site.</span></span> <span data-ttu-id="c071b-175">Добавьте приведенные ниже параметры строки запроса к URL-адресу страницы **AllItems.aspx**.</span><span class="sxs-lookup"><span data-stu-id="c071b-175">Append the following query string parameters to the URL.</span></span>

  ```
  ?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"6c5b8ee9-43ba-4cdf-a106-04857c8307be":{"location":"ClientSideExtension.ListViewCommandSet.ContextMenu","properties":{"targetUrl":"ShowDetail.aspx"}}}
  ```

  <span data-ttu-id="c071b-176">В приведенной выше строке запроса замените GUID на сохраненное ранее значение `id` из файла **CustomEcbCommandSet.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="c071b-176">In the above querystring, you will have to replace the GUID with the `id` value you saved from the **CustomEcbCommandSet.manifest.json** file.</span></span> 
  
  <span data-ttu-id="c071b-177">Кроме того, доступно свойство `location`, которое принимает значение **ClientSideExtension.ListViewCommandSet.ContextMenu**. При этом SPFx отрисовывает набор команд в виде пункта меню ECB.</span><span class="sxs-lookup"><span data-stu-id="c071b-177">Moreover, there is a `location` property which assumes the value of **ClientSideExtension.ListViewCommandSet.ContextMenu**, which instructs SPFx to render the Command Set as an ECB menu item.</span></span> <span data-ttu-id="c071b-178">Ниже представлены допустимые значения свойства `location`.</span><span class="sxs-lookup"><span data-stu-id="c071b-178">Here are all the available options for the `location` property:</span></span>
  
  * <span data-ttu-id="c071b-179">**ClientSideExtension.ListViewCommandSet.ContextMenu**.</span><span class="sxs-lookup"><span data-stu-id="c071b-179">**ClientSideExtension.ListViewCommandSet.ContextMenu**.</span></span>  <span data-ttu-id="c071b-180">Контекстное меню элементов.</span><span class="sxs-lookup"><span data-stu-id="c071b-180">ClientSideExtension.ListViewCommandSet.ContextMenu:  The context menu of the item(s)</span></span>
  * <span data-ttu-id="c071b-181">**ClientSideExtension.ListViewCommandSet.CommandBar**.</span><span class="sxs-lookup"><span data-stu-id="c071b-181">**ClientSideExtension.ListViewCommandSet.CommandBar**.</span></span> <span data-ttu-id="c071b-182">Меню верхнего уровня для набора команд в списке или библиотеке.</span><span class="sxs-lookup"><span data-stu-id="c071b-182">ClientSideExtension.ListViewCommandSet.CommandBar: The top command set menu in a list or library</span></span>
  * <span data-ttu-id="c071b-183">**ClientSideExtension.ListViewCommandSet**.</span><span class="sxs-lookup"><span data-stu-id="c071b-183">**ClientSideExtension.ListViewCommandSet**.</span></span> <span data-ttu-id="c071b-184">Контекстное меню и панель команд (соответствует параметру `SPUserCustomAction.Location="CommandUI.Ribbon"`).</span><span class="sxs-lookup"><span data-stu-id="c071b-184">`SPUserCustomAction.Location="CommandUI.Ribbon"` Both the context menu and the command bar (Corresponds to SPUserCustomAction.Location="CommandUI.Ribbon")</span></span>

  <span data-ttu-id="c071b-185">В строке запроса есть свойство `properties`, представляющее сериализацию JSON для объекта типа `ICustomEcbCommandSetProperties` (типа настраиваемых свойств, запрашиваемых настраиваемым набором команд для отрисовки).</span><span class="sxs-lookup"><span data-stu-id="c071b-185">Lastly, still in the querystring there is a property called `properties`, which represents the JSON serialization of an object of type `ICustomEcbCommandSetProperties` that is the type of the custom properties requested by the custom Command Set for rendering.</span></span>

  <span data-ttu-id="c071b-186">При выполнении запроса страницы появится предупреждающее сообщение о разрешении на запуск кода с localhost (окно с заголовком "Разрешить скрипты отладки?").</span><span class="sxs-lookup"><span data-stu-id="c071b-186">Notice that, when executing the page request, you will be prompted with a warning message box with title "Allow debug scripts?", which asks your consent to run code from localhost, for security reasons.</span></span> <span data-ttu-id="c071b-187">Конечно, если вы хотите отладить и протестировать решение локально, необходимо разрешить загрузку скриптов отладки.</span><span class="sxs-lookup"><span data-stu-id="c071b-187">Of course, if you want to locally debug and test the solution, you will have to allow to "Load debug scripts".</span></span>

<span data-ttu-id="c071b-188"><a name="PackageAndHostCommandSet"> </a></span><span class="sxs-lookup"><span data-stu-id="c071b-188"></span></span>

## <a name="package-and-host-the-solution"></a><span data-ttu-id="c071b-189">Упаковка и размещение решения</span><span class="sxs-lookup"><span data-stu-id="c071b-189">Package and host the solution</span></span>

<span data-ttu-id="c071b-190">Если вы довольны результатом, теперь можно упаковать решение и разместить его в настоящей инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="c071b-190">If you are happy with the result, you are now ready to package the solution and host it in a real hosting infrastructure.</span></span>
<span data-ttu-id="c071b-191">Прежде чем собирать пакет, необходимо объявить XML-файл Feature Framework для подготовки расширения.</span><span class="sxs-lookup"><span data-stu-id="c071b-191">Before building the bundle and the package, you need to declare an XML feature framework file to provision the extension.</span></span>

### <a name="review-feature-framework-elements"></a><span data-ttu-id="c071b-192">Обзор элементов Feature Framework</span><span class="sxs-lookup"><span data-stu-id="c071b-192">Review feature framework elements</span></span>

1. <span data-ttu-id="c071b-193">В редакторе кода откройте вложенную папку **/sharepoint/assets** в папке решения и измените файл **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="c071b-193">Within the code editor, open the **/sharepoint/assets** sub-folder of the solution folder and edit the **elements.xml** file.</span></span> <span data-ttu-id="c071b-194">В приведенном ниже фрагменте кода показано, как должен выглядеть файл.</span><span class="sxs-lookup"><span data-stu-id="c071b-194">In the following code excerpt you can see how the file should look like.</span></span>

  ```XML
  <?xml version="1.0" encoding="utf-8"?>
  <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <CustomAction
          Title="CustomEcb"
          RegistrationId="101"
          RegistrationType="List"
          Location="ClientSideExtension.ListViewCommandSet.ContextMenu"
          ClientSideComponentId="6c5b8ee9-43ba-4cdf-a106-04857c8307be"
          ClientSideComponentProperties="{&quot;targetUrl&quot;:&quot;ShowDetails.aspx&quot;}">
      </CustomAction>
  </Elements>
  ```

  <span data-ttu-id="c071b-195">Как видите, он напоминает файл SharePoint Feature Framework из "классической" модели, но использует атрибут `ClientSideComponentId` для обращения к `id` настраиваемого расширения, а также атрибут `ClientSideComponentProperties` для настройки специальных свойств конфигурации, необходимых расширению.</span><span class="sxs-lookup"><span data-stu-id="c071b-195">As you can see, it reminds the SharePoint Feature Framework file that we saw in the "classic" model, but it uses the `ClientSideComponentId` attribute to reference the `id` of the custom extension, and the `ClientSideComponentProperties` attribute, to configure the custom configuration properties required by the extension.</span></span>

2. <span data-ttu-id="c071b-196">Откройте файл **package-solution.json** в папке **/config** решения.</span><span class="sxs-lookup"><span data-stu-id="c071b-196">Now, open the **package-solution.json** file under the **/config** folder of the solution.</span></span> <span data-ttu-id="c071b-197">В файле вы увидите ссылку на файл **elements.xml** в разделе `assets`.</span><span class="sxs-lookup"><span data-stu-id="c071b-197">Within the file you can see that there is a reference to the **elements.xml** file, within the `assets` section.</span></span>

  ```JSON
  {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
      "name": "spfx-ecb-extension-client-side-solution",
      "id": "b8ff6fdf-16e9-4434-9fdb-eac6c5f948ee",
      "version": "1.0.2.0",
      "features": [
        {
          "title": "Custom ECB Menu Item.",
          "description": "Deploys a custom ECB menu item sample extension",
          "id": "f30a744c-6f30-4ccc-a428-125a290b5233",
          "version": "1.0.0.0",
          "assets": {
            "elementManifests": [
              "elements.xml"
            ]
          }
        }
      ]
    },
    "paths": {
      "zippedPackage": "solution/spfx-ecb-extension.sppkg"
    }
  }
  ```

### <a name="enable-the-cdn-in-your-office-365-tenant"></a><span data-ttu-id="c071b-198">Включение сети доставки содержимого (CDN) в клиенте Office 365</span><span class="sxs-lookup"><span data-stu-id="c071b-198">Enable the CDN in your Office 365 tenant</span></span>

<span data-ttu-id="c071b-199">Теперь необходимо разместить расширение в среде внешнего размещения.</span><span class="sxs-lookup"><span data-stu-id="c071b-199">Now you need to host the extension in a hosting environment.</span></span> <span data-ttu-id="c071b-200">Сеть доставки содержимого Office 365 — самый простой способ размещать решения SharePoint непосредственно из их клиента, пользуясь при этом преимуществами службы сетей доставки содержимого (CDN) для сокращения времени загрузки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c071b-200">Office 365 CDN is the easiest way to host SharePoint Framework solutions directly from your tenant while still taking advantage of the Content Delivery Network (CDN) service for faster load times of your assets.</span></span>

1. <span data-ttu-id="c071b-201">Скачайте [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588), чтобы убедиться, что у вас установлена последняя версия.</span><span class="sxs-lookup"><span data-stu-id="c071b-201">Download the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) to ensure that you have the latest version.</span></span>

2. <span data-ttu-id="c071b-202">Подключитесь к клиенту SharePoint Online с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c071b-202">Connect to your SharePoint Online tenant by using PowerShell:</span></span>
    
    ```powershell
    Connect-SPOService -Url https://[tenant]-admin.sharepoint.com
    ```
    
3. <span data-ttu-id="c071b-203">Чтобы узнать текущее состояние настроек общедоступной сети CDN для клиента, поочередно выполните указанные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="c071b-203">Get the current status of public CDN settings from the tenant level by executing the following commands one-by-one:</span></span> 
    
    ```powershell
    Get-SPOTenantCdnEnabled -CdnType Public
    Get-SPOTenantCdnOrigins -CdnType Public
    Get-SPOTenantCdnPolicies -CdnType Public
    ```
    
4. <span data-ttu-id="c071b-204">Включите общедоступную сеть доставки содержимого в клиенте:</span><span class="sxs-lookup"><span data-stu-id="c071b-204">Enable public CDN in the tenant:</span></span>
    
    ```powershell
    Set-SPOTenantCdnEnabled -CdnType Public
    ```
    
    <span data-ttu-id="c071b-205">Теперь в клиенте включена общедоступная сеть доставки содержимого с использованием разрешенной конфигурации типов файлов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c071b-205">Public CDN has now been enabled in the tenant by using the default file type configuration allowed.</span></span> <span data-ttu-id="c071b-206">Это означает, что поддерживаются такие расширения: CSS, EOT, CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF и WOFF.</span><span class="sxs-lookup"><span data-stu-id="c071b-206">This means that the following file type extensions are supported: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF, and WOFF.</span></span>

5. <span data-ttu-id="c071b-p126">Откройте браузер и перейдите к семейству веб-сайтов, в котором вы хотите разместить свою библиотеку CDN. Это может быть любое семейство веб-сайтов в клиенте. Это руководство описывает создание библиотеки CDN, но вы также можете использовать отдельную папку в любой существующей библиотеке документов как конечную точку CDN.</span><span class="sxs-lookup"><span data-stu-id="c071b-p126">Open up a browser and move to a site collection where you'd like to host your CDN library. This could be any site collection in your tenant. In this tutorial, we create a specific library to act as your CDN library, but you can also use a specific folder in any existing document library as the CDN endpoint.</span></span>

6. <span data-ttu-id="c071b-210">В семействе веб-сайтов создайте библиотеку документов **CDN** и добавьте в нее папку **customecb**.</span><span class="sxs-lookup"><span data-stu-id="c071b-210">Create a new document library on your site collection called **CDN** and add a folder named **customecb** to it.</span></span>
    
7. <span data-ttu-id="c071b-211">В консоли PowerShell добавьте новый источник сети доставки содержимого.</span><span class="sxs-lookup"><span data-stu-id="c071b-211">In the PowerShell console, add a new CDN origin.</span></span> <span data-ttu-id="c071b-212">В этом случае мы задаем источник `*/cdn`, то есть в качестве источника сети доставки содержимого будет выступать любая относительная папка с именем **cdn**.</span><span class="sxs-lookup"><span data-stu-id="c071b-212">In this case, we are setting the origin as `*/cdn`, which means that any relative folder with the name of **cdn** acts as a CDN origin.</span></span>
    
    ```powershell
    Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
    ```
    
8. <span data-ttu-id="c071b-213">Выполните указанную ниже команду, чтобы получить список источников сети доставки содержимого клиента:</span><span class="sxs-lookup"><span data-stu-id="c071b-213">Execute the following command to get the list of CDN origins from your tenant:</span></span>
    
    ```powershell
    Get-SPOTenantCdnOrigins -CdnType Public
    ```
    
  <span data-ttu-id="c071b-214">Обратите внимание на то, что новый источник указан как допустимый источник сети доставки содержимого.</span><span class="sxs-lookup"><span data-stu-id="c071b-214">Note that your newly added origin is listed as a valid CDN origin.</span></span> <span data-ttu-id="c071b-215">Окончательная настройка источника занимает приблизительно 15 минут, поэтому мы можем продолжить подготовку расширения, которое будет размещено в источнике после развертывания.</span><span class="sxs-lookup"><span data-stu-id="c071b-215">Final configuration of the origin takes approximately 15 minutes, so we can continue provisioning the extension, which will be hosted from the origin after deployment is completed.</span></span> 

  ![Список общедоступных источников в клиенте](../../../images/ext-app-cdn-origins-pending.png)

  <span data-ttu-id="c071b-217">Если рядом с названием источника нет уведомления `(configuration pending)`, он готов к использованию в клиенте.</span><span class="sxs-lookup"><span data-stu-id="c071b-217">When the origin is listed without the `(configuration pending)` text, it is ready to be used in your tenant.</span></span> <span data-ttu-id="c071b-218">Это указывает на выполняющуюся настройку SharePoint Online и системы CDN.</span><span class="sxs-lookup"><span data-stu-id="c071b-218">This indicates an on-going configuration between SharePoint Online and the CDN system.</span></span> 

### <a name="update-the-solution-settings-and-publish-it-on-the-cdn"></a><span data-ttu-id="c071b-219">Обновление параметров решения и его публикация в сети доставки содержимого</span><span class="sxs-lookup"><span data-stu-id="c071b-219">Update the solution settings and publish it on the CDN</span></span>

<span data-ttu-id="c071b-220">Теперь необходимо обновить решение для использования только что созданной сети CDN в качестве среды внешнего размещения и опубликовать в ней пакет решения.</span><span class="sxs-lookup"><span data-stu-id="c071b-220">Now, you need to update the solution in order to use the just created CDN as the hosting enviroment and you will need to publish the solution bundle to the CDN.</span></span> <span data-ttu-id="c071b-221">Для этого выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="c071b-221">To accomplish this task, just follow the upcoming steps.</span></span>

1. <span data-ttu-id="c071b-222">Вернитесь к ранее созданному решению, чтобы внести необходимые изменения в URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="c071b-222">Return to the previously created solution to perform the needed URL updates.</span></span>
    
2. <span data-ttu-id="c071b-223">Обновите файл **write-manifestests.json** (в папке **config**), как показано ниже, чтобы он указывал на конечную точку CDN.</span><span class="sxs-lookup"><span data-stu-id="c071b-223">Update the **write-manifests.json** file (under the **config** folder) as follows to point to your CDN endpoint.</span></span> <span data-ttu-id="c071b-224">Используйте `publiccdn.sharepointonline.com` в качестве префикса, а затем дополните URL-адрес фактическим путем к клиенту.</span><span class="sxs-lookup"><span data-stu-id="c071b-224">Use `publiccdn.sharepointonline.com` as the prefix, and then extend the URL with the actual path of your tenant.</span></span> <span data-ttu-id="c071b-225">Формат URL-адреса для сети доставки содержимого:</span><span class="sxs-lookup"><span data-stu-id="c071b-225">The format of the CDN URL is as follows:</span></span>
    
    ```
    https://publiccdn.sharepointonline.com/[tenant host name]/sites/[site]/[library]/[folder]
    ```
    
    ![Путь к конечной точке CDN в манифесте записи](../../../images/spfx-ecb-extension-write-manifest.png)

3. <span data-ttu-id="c071b-227">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="c071b-227">Save your changes.</span></span>

4. <span data-ttu-id="c071b-228">Выполните описанную ниже задачу для упаковки решения.</span><span class="sxs-lookup"><span data-stu-id="c071b-228">Execute the following task to bundle your solution.</span></span> <span data-ttu-id="c071b-229">При этом будет выполнена сборка конечной версии проекта с использованием URL-адреса сети доставки содержимого, указанного в файле **writer-manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="c071b-229">This executes a release build of your project using the CDN URL specified in the **write-manifests.json** file.</span></span> <span data-ttu-id="c071b-230">Результат будет помещен в папку **./temp/deploy**.</span><span class="sxs-lookup"><span data-stu-id="c071b-230">The output of this command is located in the **./temp/deploy** folder.</span></span> <span data-ttu-id="c071b-231">Эти файлы вам нужно будет добавить в папку SharePoint, представляющую собой конечную точку CDN.</span><span class="sxs-lookup"><span data-stu-id="c071b-231">These are the files that you need to upload to the SharePoint folder acting as your CDN endpoint.</span></span> 
    
    ```
    gulp bundle --ship
    ```
    
5. <span data-ttu-id="c071b-232">Выполните приведенную ниже задачу, чтобы упаковать решение.</span><span class="sxs-lookup"><span data-stu-id="c071b-232">Execute the following task to package your solution.</span></span> <span data-ttu-id="c071b-233">Эта команда создаст пакет **spfx-ecb-extension.sppkg** в папке **sharepoint/solution** и подготовит ресурсы в папке **temp/deploy** к развертыванию в CDN.</span><span class="sxs-lookup"><span data-stu-id="c071b-233">This command creates an **spfx-ecb-extension.sppkg** package in the **sharepoint/solution** folder and also prepares the assets in the **temp/deploy** folder to be deployed to the CDN.</span></span>
    
    ```
    gulp package-solution --ship
    ```
    
6. <span data-ttu-id="c071b-234">Добавьте или перетащите новый пакет клиентского решения в каталог приложений в клиенте, а затем нажмите кнопку **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="c071b-234">Upload or drag-and-drop the newly created client-side solution package to the app catalog in your tenant, and then select the **Deploy** button.</span></span>

    ![Диалоговое окно доверия в каталоге приложений с путем к конечной точке CDN](../../../images/spfx-ecb-extension-cdn-address.png)

7. <span data-ttu-id="c071b-236">Отправьте или перетащите файлы из папки **temp/deploy** в созданную ранее папку **CDN/customfooter**.</span><span class="sxs-lookup"><span data-stu-id="c071b-236">Upload or drag-and-drop the files in the **temp/deploy** folder to the **CDN/customfooter** folder created earlier.</span></span>

<span data-ttu-id="c071b-237"><a name="InstallCommandSet"> </a></span><span class="sxs-lookup"><span data-stu-id="c071b-237"></span></span>

## <a name="install-and-run-the-solution"></a><span data-ttu-id="c071b-238">Установка и запуск решения</span><span class="sxs-lookup"><span data-stu-id="c071b-238">Install and run the solution</span></span>

1. <span data-ttu-id="c071b-239">Откройте браузер и перейдите на любой "современный" сайт.</span><span class="sxs-lookup"><span data-stu-id="c071b-239">Open the browser and navigate to any target "modern" site.</span></span>

2. <span data-ttu-id="c071b-240">Перейдите на страницу **Контент сайта** и добавьте новое **приложение**.</span><span class="sxs-lookup"><span data-stu-id="c071b-240">Go to the **"Site Contents"** page and select to add a new **App**.</span></span>

3. <span data-ttu-id="c071b-241">Выберите **Из вашей организации**, чтобы просмотреть решения, доступные в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="c071b-241">Select to install a new app "From Your Organization" to browse the solutions available in the AppCatalog.</span></span>

4. <span data-ttu-id="c071b-242">Выберите решение **spfx-ecb-extension-client-side-solution** и установите его на целевом сайте.</span><span class="sxs-lookup"><span data-stu-id="c071b-242">Select the solution called **"spfx-custom-field-extension-client-side-solution"** and istall it on the target site.</span></span>

    ![Добавление пользовательского интерфейса приложения для добавления решения на сайт](../../../images/spfx-ecb-extension-add-app.png)

5. <span data-ttu-id="c071b-244">После завершения установки приложения откройте библиотеку **Документы** на сайте. Выбрав один документ, вы увидите пользовательский пункт меню ECB в действии.</span><span class="sxs-lookup"><span data-stu-id="c071b-244">Once the application installation will be completed, open the **"Documents"** library of the site and see the custom ECB menu item in action by selecting a single document.</span></span>

<span data-ttu-id="c071b-245">Поздравляем! Вы создали пункт меню ECB с помощью расширений SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="c071b-245">Enjoy your new custom ECB menu item built using the SharePoint Framework extensions!</span></span>

## <a name="see-also"></a><span data-ttu-id="c071b-246">См. также</span><span class="sxs-lookup"><span data-stu-id="c071b-246">See also</span></span>

- [<span data-ttu-id="c071b-247">Обзор расширений SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="c071b-247">Overview of SharePoint Framework Extensions</span></span>](../overview-extensions.md)
