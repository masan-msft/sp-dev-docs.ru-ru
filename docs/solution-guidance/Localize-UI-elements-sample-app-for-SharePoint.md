---
title: "Локализация пользовательского интерфейса элементов пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: e97db9ff902347015c47cfdb6605ec74072459ed
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="localize-ui-elements-sample-add-in-for-sharepoint"></a>Локализация пользовательского интерфейса элементов пример надстройки для SharePoint

Элементы пользовательского интерфейса SharePoint можно локализовать с помощью JavaScript для замены текстовое значение значение элемента пользовательского интерфейса со значением переведенный текст, загруженными из файла ресурсов JavaScript. 

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_
    
Пример надстройки [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) показано, как использовать JavaScript для замены текстового значения элементов пользовательского интерфейса SharePoint со значением переведенный текст, который считываются из файла ресурсов JavaScript. 

**Примечание**  Вы несете ответственность за обеспечение значения переведенный текст в файле ресурсов JavaScript. 

В этом примере код использует размещение у поставщика в надстройке для:

- Локализация страница сайта или панели быстрого запуска ссылку заголовка с определенным текстовые значения.
    
- Сохранить страницу сайта или панели быстрого запуска ссылку заголовка в основной язык, а также предоставлять переведенные версии веб-страницы и панели быстрого запуска title ссылку на другом языке во время выполнения.
    
- Использование файлов ресурсов JavaScript для локализации со стороны клиента.
    
- Ссылка на файл JavaScript на сайте SharePoint, с помощью дополнительного действия.
    
- Проверьте региональные параметры пользовательского интерфейса веб-узла, а затем загружать значения текста для конкретного языка и региональных параметров из файла ресурсов JavaScript.
    
- Замените значения текста для конкретного языка и региональных параметров с помощью jQuery страница сайта и заголовки ссылок на панели быстрого запуска.

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Прежде чем запустить этот пример кода Настройка языковых параметров на вашем сайте и задать язык отображения на странице профиля пользователя.

### <a name="to-configure-the-language-settings-on-your-site"></a>Настройка языковых параметров сайта

1. На сайте группы выберите **Параметры** > **Параметры сайта**.
    
2. **Администрирование веб-сайтов**выберите **языковые параметры**.
    
3. На странице **Языковых параметров** в **Альтернативные языки**выберите альтернативные языки, которые должны поддерживать веб-узла. Например выберите **французский** и **финский**, как показано на рисунке 1.
    
4. Нажмите кнопку  **ОК**.

### <a name="to-set-the-display-language-on-your-users-profile-page"></a>Чтобы задать язык отображения на странице профиля пользователя

1. В верхней части сайта Office 365 выберите изображение профиля и выберите команду **сведения обо мне,** как показано на рисунке 2.
    
2. На странице " **сведения обо мне** " нажмите кнопку **Изменить профиль**.
    
3. Нажмите кнопку с многоточием (...) для Дополнительные параметры и затем выберите **языка и региона**.
    
4. На **Мой языки**нажмите кнопку Новый язык в раскрывающемся списке **выбрать новый язык** и нажмите кнопку **Добавить**. Например выберите французский и финский, как показано на рисунке 3. Может потребоваться перемещение предпочитаемый язык вверх или вниз, выбрав вверх и вниз стрелки.
    
5. Выберите команду **Сохранить все и закрыть**.

**Примечание**  Выполнение может занять несколько минут для сайта отобразить в выбранные языки.

**Важные**  CSOM периодически добавлены новые функции. Если CSOM предоставляет новые функции для обновления веб-страницы или панели быстрого запуска заголовки ссылок, рекомендуется использовать новые возможности в CSOM вместо описанные здесь.

**На рисунке 1. Настройка языка для сайта**

![Снимок экрана, на странице параметров языковых параметров сайта](media/0265dd57-cf25-4879-a6df-68072ffa5270.png)

**На рисунке 2. Переход к странице профиля пользователя, выбрав сведения обо мне**

![Снимок экрана страницы профиля пользователя с помощью сведения обо мне с выделением](media/e3971203-7011-40ad-ab1b-341af2df28fc.png)

**На рисунке 3. Изменение языка интерфейса пользователя на странице профиля пользователя**

![Снимок экрана раздела языка и региона на странице "Изменение сведений"](media/ff41b24e-42eb-48ca-83cd-00d88ef753bd.png)

Прежде чем запускать [сценарии 2](#bk_Scenario2) этот пример кода, выполните следующие задачи.

### <a name="to-create-a-quick-launch-link"></a>Создание ссылки на панели быстрого запуска

1. На хост-сайта выберите команду **Изменить СВЯЗИ**.
    
2. Выберите **ссылку**, как показано на рисунке 4.
    
3. В **текст для отображения**введите **Моя запись панели быстрого запуска**.
    
4. В поле **адрес**введите URL-адрес веб-сайта.
    
5. Нажмите **кнопку ОК,** > **Сохранить**.

**На рисунке 4. Добавление ссылки на панели быстрого запуска**

![Снимок экрана, на странице Изменение СВЯЗЕЙ со ссылкой на с выделением](media/fcb28647-1576-4e86-8ca7-15f3ce8d85fb.png)

### <a name="to-create-a-site-page"></a>Создание страницы сайта

1. На веб-сайт, щелкните **Содержимое сайта** > **Страниц сайта** > **новый**.
    
2. В поле **новое имя страницы** введите **Hello SharePoint**.
    
3. Нажмите кнопку **Создать**.
    
4. Введите **Тестовая страница** в теле страницы.
    
5. Выберите команду **Сохранить**.

## <a name="using-the-corejavascriptcustomization-sample-app"></a>Использование примера приложения Core.JavaScriptCustomization
<a name="sectionSection1"> </a>

При запуске в этом примере отображается приложение, размещаемое у поставщика как показано на рисунке 5. В этой статье описаны сценарии 1 и 2 сценарий способов, описанных в сценарии 1 и 2 сценарий может использовать для предоставления локализованных версий страницы сайта и заголовки ссылок на панели быстрого запуска. 

**На рисунке 5. Начальная страница приложения Core.JavaScriptCustomization**

![Снимок экрана, показывающий начальной странице Core.JavaScriptCustomization приложения](media/133a6c15-7b96-4418-b795-a7bdab63ead4.png)
### <a name="scenario-1"></a>Сценарий 1

Сценарий 1 показано, как добавить ссылку на файл JavaScript на сайте SharePoint, с помощью дополнительного действия. Кнопки **параметров вставки** вызывает метод **btnSubmit_Click** в scenario1.aspx.cs. Метод **btnSubmit_Click** вызывает **AddJsLink** для добавления ссылки на файлы JavaScript, с помощью дополнительного действия на хост-сайта.

На рисунке 6 показан на начальной странице сценарии 1.

**На рисунке 6. Сценарий 1 начальной страницы**

![Снимок экрана с начальной страницы для сценария 1](media/16972165-5f94-497f-b58c-0e1075d9616a.png)

Метод **AddJSLink** является частью файла JavaScriptExtensions.cs в **OfficeDevPnP.Core**.  **AddJSLink** требуется указать строку, представляющую идентификатор для назначения настраиваемого действия, что строка, содержащая точку с запятой запятыми список URL-адресов для файлов JavaScript, которые вы хотите добавить в веб-сайт. Обратите внимание, что этот пример кода добавляет ссылку на Scripts\scenario1.js, который добавляет сообщение о состоянии панели веб-сайт.
    
**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```
protected void btnSubmit_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var cc = spContext.CreateUserClientContextForSPHost())
            {
                cc.Web.AddJsLink(Utilities.Scenario1Key, Utilities.BuildScenarioJavaScriptUrl(Utilities.Scenario1Key, this.Request));
            }
        }
```
   
**Примечание**  SharePoint 2013 с помощью стратегия минимальной загрузки для сокращения объема данных, браузер загружает при переходе между страницами на сайте SharePoint. [Стратегия минимальной загрузки](http://msdn.microsoft.com/library/9caa7d99-1e74-4889-96c7-ba5a10772ad7.aspx)Дополнительные сведения см. В scenario1.js следующий код гарантирует, что ли стратегия минимальной загрузки используется на сайте SharePoint, этот метод **RemoteManager_Inject** всегда вызывается для запуска кода JavaScript для добавления панели сообщение о состоянии хост-сайта.

```
if ("undefined" != typeof g_MinimalDownload &amp;&amp; g_MinimalDownload &amp;&amp; (window.location.pathname.toLowerCase()).endsWith("/_layouts/15/start.aspx") &amp;&amp; "undefined" != typeof asyncDeltaManager) {
    // Register script for MDS if possible.
    RegisterModuleInit("scenario1.js", RemoteManager_Inject); //MDS registration
    RemoteManager_Inject(); //non MDS scenario
} else {
    RemoteManager_Inject();
}
```

**Примечание**  Некоторые файлы JavaScript может зависеть от других файлов JavaScript для загрузки во-первых, прежде чем их можно было запустить и выполнить операцию. Следующая конструкция кода из **RemoteManager_Inject** используется функция **loadScript** в scenario1.js для первой загрузки jQuery, а затем продолжить выполнение оставшийся код JavaScript.

```
var jQuery = "https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js";

    // Load jQuery first, then continue running the rest of the code.
    loadScript(jQuery, function () {
     // Add additional JavaScript code here to complete your task. 
});
```

Выберите **веб-узел**. Как показано на рисунке 7, веб-сайт теперь отображается сообщение о состоянии панели, который был добавлен с scenario1.js.

**На рисунке 7. Сообщение о состоянии панели, добавленных на сайт группы, с помощью JavaScript**

![Снимок экрана с сообщением панели состояния, добавленных на сайт группы с помощью JavaScript](media/c5d6fb6d-f05f-49aa-a3c5-af1240ee9135.png)

### <a name="scenario-2"></a>Сценарий 2
<a name="bk_Scenario2"> </a>

Сценарий 2 использует метод, описанный в сценарии 1 замена текста пользовательского интерфейса на чтение из файла ресурсов JavaScript переведенный текст. Сценарий 2 заменяет заголовок панели быстрого запуска ссылку ( **Моя запись панели быстрого запуска**) и сайт страницы заголовка ( **Hello SharePoint**), созданного ранее. Сценарий 2 подключает файл JavaScript, которые переведенного текстовые значения из переменных в допустимом формате файлов ресурсов JavaScript. Сценарий 2 обновляет пользовательский Интерфейс. На рисунке 8 показана начальная страница для сценария 2.

**На рисунке 8. Сценарий 2 начальной страницы**

![Снимок экрана с начальной страницы для сценария 2](media/c706060b-e77d-4ae6-99c4-43dee80ff7d3.png)

Как показано на рисунке 8, выбор **параметров вставки** применяются следующие изменения к сайту:

- Заголовок панели быстрого запуска ссылку **Моя запись панели быстрого запуска** изменяется на **Contoso ссылок**.
    
- Заголовок страницы сайта **Hello SharePoint** изменяется на **Contoso страницы**.

**На рисунке 9. Сценарий 2 настроек**

![Сценарий 2 настроек](media/47e8ec40-d291-496f-8677-01eb46441df2.png)
    
**Примечание**  Если необходимые значения для быстрого запуска ссылку название и заголовок страницы сайта, отличаются от условий показано на рисунке 8 изменить переменные **quickLauch_Scenario2** и **pageTitle_HelloSharePoint** в ресурсов JavaScript файлы scenario2.en us.js или scenario2.NL-nl.js. Затем снова запустите пример кода. В файле scenario2.en us.js хранятся ресурсы для конкретного языка и региональных параметров Английский (США). В файле scenario2.nl nl.js хранятся голландский ресурсы для конкретного языка и региональных параметров. При тестировании этот пример кода, использующий другой язык, рассмотрите возможность создания другой файл ресурсов JavaScript, с помощью же соглашение об именовании.

Как и в сценарии 1, **btnSubmit_Click** в scenario2.aspx.cs вызывает **AddJsLink** , чтобы добавить ссылку на файл Scripts\scenario2.js. В scenario2.js функция **RemoteManager_Inject** вызывает функцию **TranslateQuickLaunch** , которая выполняет следующие задачи:

- Определяет узел языка и региональных параметров с помощью **_spPageContextInfo.currentUICultureName**.
    
- Загружает файл ресурсов JavaScript, содержащий ресурсы конкретного языка и региональных параметров, которые соответствуют языка и региональных параметров пользовательского интерфейса веб-узла. Например если язык и региональные параметры веб-узла русский (Россия), загрузки файла scenario2.en us.js.
    
- Заменяет значение переменной **quickLauch_Scenario2** , чтение из файлов ресурсов JavaScript **Моя запись панели быстрого запуска** .

```
function RemoteManager_Inject() {

    var jQuery = "https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js";
    
    loadScript(jQuery, function () {
        SP.SOD.executeOrDelayUntilScriptLoaded(function () { TranslateQuickLaunch(); }, 'sp.js');
    });
}

function TranslateQuickLaunch() {
    // Load jQuery and if complete, load the JS resource file.
    var scriptUrl = "";
    var scriptRevision = "";
    // iterate over the scripts loaded on the page to find the scenario2 script. Then use the script URL to dynamically build the URL for the resource file to be loaded.
    $('script').each(function (i, el) {
        if (el.src.toLowerCase().indexOf('scenario2.js') > -1) {
            scriptUrl = el.src;
            scriptRevision = scriptUrl.substring(scriptUrl.indexOf('.js') + 3);
            scriptUrl = scriptUrl.substring(0, scriptUrl.indexOf('.js'));
        }
    })

    var resourcesFile = scriptUrl + "." + _spPageContextInfo.currentUICultureName.toLowerCase() + ".js" + scriptRevision;
    // Load the JS resource file based on the user's language settings.
    loadScript(resourcesFile, function () {

        // General changes that apply to all loaded pages.
        // ----------------------------------------------

        // Update the Quick Launch labels.
        // Note that you can use the jQuery  function to iterate over all elements that match your jQuery selector.
        $("span.ms-navedit-flyoutArrow").each(function () {
            if (this.innerText.toLowerCase().indexOf('my quicklaunch entry') > -1) {
                // Update the label.
                $(this).find('.menu-item-text').text(quickLauch_Scenario2);
                // Update the tooltip.
                $(this).parent().attr("title", quickLauch_Scenario2);
            }
        });

        // Page specific changes require an IsOnPage call.
        // ----------------------------------------------------------

        // Change the title of the "Hello SharePoint" page.
        if (IsOnPage("Hello%20SharePoint.aspx")) {
            $("#DeltaPlaceHolderPageTitleInTitleArea").find("A").each(function () {
                if ($(this).text().toLowerCase().indexOf("hello sharepoint") > -1) {
                    // Update the label.
                    $(this).text(pageTitle_HelloSharePoint);
                    // Update the tooltip.
                    $(this).attr("title", pageTitle_HelloSharePoint);
                }
            });
        }

    });
}
```

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Локализация решения для SharePoint 2013 и SharePoint Online](localization-solutions-for-sharepoint-2013-and-sharepoint-online.md)
    
-  [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)
