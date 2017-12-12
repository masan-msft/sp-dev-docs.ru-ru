---
title: "Используйте возможности локализации в Office 365 пример надстройки"
ms.date: 11/03/2017
ms.openlocfilehash: e3f6644f841f53b8e62e95ed626477aef0b0ac6b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="use-localization-features-in-office-365-sample-add-in"></a>Используйте возможности локализации в Office 365 пример надстройки

Можно использовать возможности локализации в Office 365 для предоставления локализованных значений для сайтов, списков, типов контента и столбцы сайта SharePoint. 
    
_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_
    
Пример [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes) показано, как использовать возможности локализации Office 365 на сайты, списки, типы контента и столбцы сайта. В этом образце кода используется консольного приложения для выполнения следующих:

- Создание типов контента, столбцы сайтов и списков и свяжите столбцы сайта с помощью типов содержимого.
    
- Локализация типа контента, столбец сайта, списка и сайта, предоставленный пользователем.

> [!NOTE] 
> Локализация компонентов, описанных в этой статье доступны только в Office 365. Сведения о возможности локализации, доступные в Office 365 выделенных или SharePoint Server 2013 в локальной можно [как: локализация надстроек для SharePoint](http://msdn.microsoft.com/library/907a9189-7ce3-469a-8c87-4cef26f03c73.aspx) и [решений SharePoint локализации](https://msdn.microsoft.com/en-us/library/ee696750.aspx).

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Прежде чем запускать этот пример кода:

1. Настройка языковых параметров на вашем сайте. Для этого сделайте следующее.
    
      . На сайте группы выберите **Параметры** > **Параметры сайта**.
    
      б. **Администрирование веб-сайтов**выберите **языковые параметры**.
    
      c. На странице **Языковых параметров** в **Альтернативные языки**выберите альтернативные языки, которые должны поддерживать веб-узла. Например вы можете французский и финский, как показано на рисунке 1.
    
      d. Нажмите кнопку  **ОК**.
     
2. Задайте язык отображения на странице профиля пользователя. Для этого сделайте следующее.
    
      . В верхней части сайта Office 365 выберите изображение профиля и выберите команду **сведения обо мне**, как показано на рисунке 2.
    
      б. На странице " **сведения обо мне** " нажмите кнопку **Изменить профиль**.
    
      c. Выберите **...** (Дополнительные параметры) и затем выберите **языка и региона**.
    
      d. На **Мой языки**, нажмите кнопку Новый язык, аналогичный тому, задайте на сайте, используя раскрывающийся список **выбрать новый язык** , нажмите кнопку **Добавить**. Например выберите французский и финский, как показано на рисунке 3. Вы можете переместить предпочитаемый язык вверх или вниз, выбрав вверх и вниз стрелки.
    
      e. Выберите команду **Сохранить все и закрыть**.

> [!NOTE] 
> Выполнение может занять несколько минут для сайта отобразить в выбранные языки. 

**На рисунке 1. Языковые параметры для сайта**

![Снимок экрана, который отображает параметры языка для сайта.](media/ffe149ae-17ab-4c55-a611-d47f4eb88c4e.png)

**На рисунке 2. Переход к странице профиля пользователя, выбрав сведения обо мне**

![Снимок экрана страницы профиля пользователя с помощью сведения обо мне с выделением](media/764b2ac2-155b-4ce9-b8eb-3ae04ad26593.png)

**На рисунке 3. Изменение языка интерфейса пользователя на странице профиля пользователя**

![Снимок экрана в разделе языка и региона страницы профиля](media/ae5f565d-c932-43dd-9dc3-87630cee3692.png)

## <a name="using-the-corecreatecontenttypes-sample-app"></a>Использование примера приложения Core.CreateContentTypes
<a name="sectionSection1"> </a>

При запуске в этом примере кода отображаются консольного приложения как показано на рисунке 4. Необходимо предоставить учетные данные администратора Office 365 и сайта для локализации. После запуска консольного приложения в метод **Main** в файле Program.cs выполняет следующие задачи:

- Вызывает метод **CreateContentTypeIfDoesNotExist** , чтобы создать тип контента с именем **Contoso документа**.
    
- Вызывает метод **CreateSiteColumn** , чтобы создать столбец сайта с именем **Contoso строки**.
    
- Вызывает метод **AddSiteColumnToContentType** , чтобы связать столбец сайта **Contoso строки** с типом контента **Документа Contoso** .
    
- Вызывает метод **CreateCustomList** , чтобы создать новый список с именем **MyList**.

**На рисунке 4. Core.CreateContentTypes консольного приложения**

![Снимок экрана с Core.CreateContentTypes консольного приложения](media/ee806481-0089-4c65-8f8b-027bfff6ddb9.png)

Метод **Main** вызывает методы **LocalizeSiteAndList** и **LocalizeContentTypeAndField** . Метод **LocalizeSiteAndList** демонстрирует выполните следующее:

- Установить разные локализованные значения для заголовок и описание сайта, с помощью метода **SetValueForUICulture** на свойства **TitleResource** и **DescriptionResource** на **веб-** объект.
    
- Установить разные локализованные значения для заголовок и описание сайта, с помощью метода **SetValueForUICulture** на свойства **TitleResource** и **DescriptionResource** на **веб-** объект.
    
Метод **LocalizeContentTypeAndField** демонстрирует выполните следующее:

- Установить разные локализованные значения для имени и описания типа контента с помощью метода **SetValueForUICulture** на **NameResource** и **DescriptionResource** свойств объекта **ContentType** .
    
- Установить разные локализованные значения для заголовок и описание сайта, с помощью метода **SetValueForUICulture** на **TitleResource** и **DescriptionResource** свойств объекта **поля** .
    
> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
private static void LocalizeSiteAndList(ClientContext cc, Web web)
        {
            // Localize the site title.
            web.TitleResource.SetValueForUICulture("en-US", "Hello World");
            web.TitleResource.SetValueForUICulture("fi-FI", "Hello World - Finnish");
            web.TitleResource.SetValueForUICulture("fr-FR", "Hello World - French");
            // Localize the site description.
            web.DescriptionResource.SetValueForUICulture("en-US", "Hello World site sample");
            web.DescriptionResource.SetValueForUICulture("fi-FI", " Hello World site sample - Finnish");
            web.DescriptionResource.SetValueForUICulture("fr-FR", " Hello World site sample - French");
            web.Update();
            cc.ExecuteQuery();

            // Localize the custom list that was created previously.
            List list = cc.Web.Lists.GetByTitle("MyList");
            cc.Load(list);
            cc.ExecuteQuery();
            // Localize the list title.
            list.TitleResource.SetValueForUICulture("en-US", "Hello World");
            list.TitleResource.SetValueForUICulture("fi-FI", "Hello World - Finnish");
            list.TitleResource.SetValueForUICulture("fr-FR", " Hello World - French");
            // Localize the list description.
            list.DescriptionResource.SetValueForUICulture("en-US", "This example localizes a list using CSOM.");
            list.DescriptionResource.SetValueForUICulture("fi-FI", "This example localizes a list using CSOM - Finnish.");
            list.DescriptionResource.SetValueForUICulture("fr-FR", "This example localizes a list using CSOM - French.");
            list.Update();
            cc.ExecuteQuery();
        }

private static void LocalizeContentTypeAndField(ClientContext cc, Web web)
        {
            ContentTypeCollection contentTypes = web.ContentTypes;
            ContentType myContentType = contentTypes.GetById("0x0101009189AB5D3D2647B580F011DA2F356FB2");
            cc.Load(contentTypes);
            cc.Load(myContentType);
            cc.ExecuteQuery();
            // Localize content type name.
            myContentType.NameResource.SetValueForUICulture("en-US", "Contoso Document");
            myContentType.NameResource.SetValueForUICulture("fi-FI", "Contoso Document - Finnish");
            myContentType.NameResource.SetValueForUICulture("fr-FR", "Contoso Document - French");
            // Localize content type description.
            myContentType.DescriptionResource.SetValueForUICulture("en-US", "This is the Contoso Document.");
            myContentType.DescriptionResource.SetValueForUICulture("fi-FI", " This is the Contoso Document - Finnish.");
            myContentType.DescriptionResource.SetValueForUICulture("fr-FR", " This is the Contoso Document - French.");
            myContentType.Update(true);
            cc.ExecuteQuery();

            // Localize the site column.
            FieldCollection fields = web.Fields;
            Field fld = fields.GetByInternalNameOrTitle("ContosoString");
            // Localize site column title.
            fld.TitleResource.SetValueForUICulture("en-US", "Contoso String");
            fld.TitleResource.SetValueForUICulture("fi-FI", "Contoso String - Finnish");
            fld.TitleResource.SetValueForUICulture("fr-FR", "Contoso String - French");
            // Localize site column description.
            fld.DescriptionResource.SetValueForUICulture("en-US", "Used to store Contoso specific metadata.");
            fld.DescriptionResource.SetValueForUICulture("fi-FI", "Used to store Contoso specific metadata - Finnish.");
            fld.DescriptionResource.SetValueForUICulture("fr-FR", "Used to store Contoso specific metadata - French.");
            fld.UpdateAndPushChanges(true);
            cc.ExecuteQuery();
        }
```

Как показано на рисунке 5, веб-узла отображает пользовательский заголовок французского **Hello World — французский**, которое было задано с помощью метода **LocalizeSiteAndList** .

**На рисунке 5. Настраиваемая страница заголовка, обновлены с помощью метода LocalizeSiteAndList**

![Снимок экрана заголовка обновленные настраиваемая страница](media/14471283-f7b6-49ca-a507-a3e28e43ee22.png)

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Локализация решения для SharePoint 2013 и SharePoint Online](localization-solutions-for-sharepoint-2013-and-sharepoint-online.md)
    
-  [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes)
    
-  [Управление контентом корпоративных решений для SharePoint 2013 и SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
