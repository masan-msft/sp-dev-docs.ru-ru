---
title: "Отправка веб-частей в SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 81cac6a20f7907a0a15edcd81bf393b896e82153
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="upload-web-parts-in-sharepoint"></a>Отправка веб-частей в SharePoint

Развертывание предварительно настроенным, стандартный SharePoint веб-частей для пользователей.

_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Можно загрузить предварительно настроенным, стандартных веб-частей SharePoint для пользователей, чтобы добавлять на свои сайты SharePoint. Например можно передать предварительно настроенный:

- Редактор сценариев веб-часть, которая использует файлы JavaScript на удаленной веб.
    
- Веб-часть поиска контента.
    
В этой статье рассматриваются предварительная настройка веб-части редактора скрипта для использования файлов JavaScript на удаленной веб-для выполнения настройки пользовательского интерфейса. Используйте для этого решения:

- Используйте в сценарии с удаленного веб-узла в веб-части, а не ссылающегося скрипты из списка **Ресурсы сайта** на хост-сайта.
    
- Развертывание предварительно настроенную веб-частей в настраиваемой процедуры подготовки сайта. Например как часть настраиваемой процедуры подготовки сайта, можно отображать сведения об использовании политики сайта для пользователя при создании нового сайта. 
    
- Автоматически Загрузите содержимое отфильтрованные в веб-частей для пользователей. Например файл сценария может отображать сведения местные новости, чтение из внешней системы.
    
- Разрешение пользователям самостоятельно добавлять дополнительные функции для веб-узла с помощью веб-частей из **Коллекции веб-частей**.

## <a name="before-you-begin"></a>Перед началом работы

Чтобы начать работу, загрузите пример надстройки [Core.AppScriptPart](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.AppScriptPart) из проекта [Office 365 для разработчиков шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="using-the-coreappscriptpart-add-in"></a>С помощью надстройки Core.AppScriptPart

При запуске примера кода и выберите **Запуск сценария**:

1. Выберите **веб-узел**.
    
2. **Страница**выбора > **Изменить** > **Вставка** > **веб-части**.
    
3. В **категории**нажмите кнопку **Добавить в части сценария**и выберите **данные профилей пользователей**.
    
4. Нажмите кнопку **Добавить**.
    
5. В раскрывающемся списке в правом верхнем углу веб-части **сведений профиля пользователя** выберите **Изменить веб-часть**.
    
6. Выберите **Изменить ФРАГМЕНТ**.
    
7. Просмотр ** &lt;СЦЕНАРИЙ&gt; ** элемент.
    
    Обратите внимание на то, что ссылки атрибут **src** на JavaScript файла на удаленный веб. ** &lt;СЦЕНАРИЙ&gt; ** элемент задается свойство **содержимого** в Core.AppScriptPartWeb\userprofileinformation.webpart, как показано в следующем примере. Файл JavaScript, связанный с помощью атрибута **src** — Core.AppScriptPartWeb\Scripts\userprofileinformation.js. Userprofileinformation.js считывает сведения о текущем пользователе профилей из службы профилей пользователей, а затем отображает эти сведения в веб-части.
    
    > [!NOTE] 
    > Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

  ```XML
  <property name="Content" type="string">&amp;lt;script type="text/javascript" src="https://localhost:44361/scripts/userprofileinformation.js"&amp;gt;&amp;lt;/script&amp;gt;
&amp;lt;div id="UserProfileAboutMe"&amp;gt;&amp;lt;div&amp;gt;
  </property>
  ```

8. Нажмите кнопку **Отмена**.
    
9. Нажмите кнопку **Сохранить**.

> [!NOTE] 
> Если изображения профилей пользователей не отображается, откройте OneDrive для бизнеса сайта и затем вернуться на хост-сайта.

В Core.AppScriptPartWeb\Pages\Default.aspx **Запустите сценарий** работает **btnScenario_Click**, который выполняет следующие:

1. Возвращает ссылку на **Коллекцию веб-частей** папки.
    
2. Использует [FileCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.aspx) для создания файла userprofileinformation.webpart Отправка из надстройки размещением у поставщика в **Коллекцию веб-частей**. Папка **. Files.Add** метод добавляет файл в **Коллекцию веб-частей**.
    
3. Извлекает все элементы списка в **Коллекцию веб-частей**, а затем выполняет поиск userprofileinformation.webpart.
    
4. При обнаружении userprofileinformation.webpart назначает веб-части в пользовательскую группу с именем **Add-in части скрипта**.

```C#
protected void btnScenario_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                var folder = clientContext.Web.Lists.GetByTitle("Web Part Gallery").RootFolder;
                clientContext.Load(folder);
                clientContext.ExecuteQuery();

                // Upload the "userprofileinformation.webpart" file.
                using (var stream = System.IO.File.OpenRead(
                                Server.MapPath("~/userprofileinformation.webpart")))
                {
                    FileCreationInformation fileInfo = new FileCreationInformation();
                    fileInfo.ContentStream = stream;
                    fileInfo.Overwrite = true;
                    fileInfo.Url = "userprofileinformation.webpart";
                    File file = folder.Files.Add(fileInfo);
                    clientContext.ExecuteQuery();
                }

                // Update the group that the Web Part belongs to. Start by getting all list items in the Web Part Gallery, and then find the Web Part that was just uploaded.
                var list = clientContext.Web.Lists.GetByTitle("Web Part Gallery");
                CamlQuery camlQuery = CamlQuery.CreateAllItemsQuery(100);
                Microsoft.SharePoint.Client.ListItemCollection items = list.GetItems(camlQuery);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
                foreach (var item in items)
                {
                    // Create new group.
                    if (item["FileLeafRef"].ToString().ToLowerInvariant() == "userprofileinformation.webpart")
                    {
                        item["Group"] = "add-in Script Part";
                        item.Update();
                        clientContext.ExecuteQuery();
                    }
                }

                lblStatus.Text = string.Format("add-in script part has been added to Web Part Gallery. You can find 'User Profile Information' script part under 'App Script Part' group in the <a href='{0}'>host web</a>.", spContext.SPHostUrl.ToString());
            }
        }
```

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Шаблоны и рекомендации решений разработки Office 365](Office-365-development-patterns-and-practices-solution-guidance.md)
    
- [Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md)
