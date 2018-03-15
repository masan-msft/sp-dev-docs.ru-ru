---
title: "Добавление веб-части на веб-страницу сайта надстройки"
description: "Добавьте готовую веб-часть на страницу сайта надстройки SharePoint."
ms.date: 12/20/2017
ms.prod: sharepoint
ms.openlocfilehash: 6c30611332182bc1ab5e831fab220ad8c1fb4d60
ms.sourcegitcommit: 6f2b3b5bd81c2de4f761e10ed5e2f0b9c3c485bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="include-a-web-part-on-a-webpage-in-the-add-in-web"></a>Добавление веб-части на веб-страницу сайта надстройки

Вы можете добавить готовую веб-часть на страницу сайта надстройки SharePoint, но важно делать это так, чтобы не возникало проблем с обновлением надстройки.
 
Пример кода, иллюстрирующий представленные в этой статье рекомендации: [OfficeDev/Core.WebPartOnAppWebPage](https://github.com/SharePoint/PnP/tree/master/Samples/Core.WebPartOnAppWebPage).

## <a name="add-a-web-part-to-a-page"></a>Добавление веб-части на страницу

1. Создайте в Visual Studio проект надстройки SharePoint с размещением в SharePoint. Дополнительные сведения см. в статье [Создание надстроек SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).

2. Откройте ASPX-файл, в который вы хотите добавить веб-часть. В этой статье в качестве примера используется файл Default.aspx. 
    
3. Добавьте класс **WebPartZone** в элемент `<asp:Content>`, в котором нужно указать веб-часть. Обычно его добавляют в элемент `<asp:Content>`, свойство `ContentPlaceHolderId` которого имеет значение `PlaceHolderMain`. Ниже приведен пример.
    
    ```XML
      <asp:Content ContentPlaceHolderId="PlaceHolderMain" runat="server">
        <WebPartPages:WebPartZone runat="server" FrameType="TitleBarOnly" 
          ID="HomePage1" Title="loc:full" />
      </asp:Content>
    ```

    > [!WARNING] 
    > В качестве дочернего элемента **WebPartZone** можно добавить элемент веб-части, такой как **<WebPartPages:XsltListViewWebPart>**. Но мы не рекомендуем это делать в надстройке SharePoint. Элемент веб-части, вставленный в ASPX-файл, может привести к сбою некоторых сценариев обновления. При этом отображается сообщение: "Веб-часть с таким идентификатором уже добавлена на эту страницу". Рекомендуем добавлять веб-части в манифест элементов для страницы, как описано ниже.

4. Откройте файл манифеста элементов для страницы. Обычно он называется elements.xml и находится в той же папке проекта, что и ASPX-файл.
    
5. В элементе **File** для страницы добавьте дочерний элемент **AllUsersWebPart** и задайте для его атрибута **WebPartZoneID** значение зоны веб-частей, созданной на странице. Ниже приведен пример.
    
    ```XML
      <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
        <Module Name="Pages">
          <File Path="Pages\Default.aspx" Url="Pages/Default.aspx" ReplaceContent="TRUE" >
            <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">

            </AllUsersWebPart>
          </File>
        </Module>
      </Elements>
    ```

6. Добавьте дочерний элемент **CDATA** в элемент **AllUsersWebPart**, а затем добавьте дочерний элемент **webParts** в элемент **CDATA**. Ниже приведен пример. 
    
    ```XML
      <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">
        <![CDATA[
          <webParts>

          </webParts>
        ]]>
      </AllUsersWebPart>
    ```

7. Добавьте разметку **webPart** в качестве дочернего элемента для элемента **webParts**. В приведенном ниже примере добавляется веб-часть **XsltListViewWebPart**. Предполагается, что пользовательский список "Test List" входит в состав того же проекта надстройки. Информацию о том, как добавить пользовательский список на сайт надстройки, см. в статье [Создание надстройки с размещением у поставщика, которая включает в себя настраиваемый список SharePoint и тип контента](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-conte.md). 
    
    > [!NOTE] 
    > Обратите внимание на то, что у веб-части нет свойства ID. Рекомендуем включать явный идентификатор веб-части только в двух случаях, когда это действительно необходимо. Включайте его, когда веб-часть добавляется на вики-страницу SharePoint или является одной из нескольких связанных веб-частей.

    ```XML
      <webParts>
      <webPart xmlns="http://schemas.microsoft.com/WebPart/v3">
        <metaData>
          <type name="Microsoft.SharePoint.WebPartPages.XsltListViewWebPart, 
                      Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, 
                      PublicKeyToken=71e9bce111e9429c" />
        </metaData>
        <data>
          <properties>
            <property name="ListUrl">Lists/{TestList}</property>
            <property name="IsIncluded">True</property>
            <property name="NoDefaultStyle">True</property>
            <property name="Title">{Test List}</property>
            <property name="PageType">PAGE_NORMALVIEW</property>
            <property name="Default">False</property>
            <property name="ViewContentTypeId">0x</property>
          </properties>
        </data>
      </webPart>
    </webParts>
    ```

8. Нажмите клавишу F5 для отладки надстройки. Веб-часть должна появиться на странице.
    
 
## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Создание компонентов взаимодействия с пользователем в SharePoint](create-ux-components-in-sharepoint.md)
