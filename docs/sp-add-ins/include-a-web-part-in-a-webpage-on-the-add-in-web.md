
# <a name="include-a-web-part-in-a-webpage-on-the-add-in-web"></a>Включение веб-части в веб-страницу сайта надстройки
Узнайте, как включить веб-часть в страницу надстройки SharePoint.
 

 **Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

Вы можете включить встроенную веб-часть в страницу на сайте надстройки SharePoint, но важно делать это так, чтобы не возникало проблем с обновлением надстройки.
 

Пример кода, иллюстрирующий представленные в этой статье рекомендации: [OfficeDev/Core.WebPartOnAppWebPage](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.WebPartOnAppWebPage)
 


## <a name="prerequisites"></a>Необходимые компоненты

Предварительные требования указаны в статье [Знакомство с созданием надстроек SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins).
 

 

## <a name="add-a-web-part-to-a-page"></a>Добавление веб-части на страницу


 

 

1. Создайте надстройку, размещаемую в SharePoint, с помощью Visual Studio. Дополнительные сведения см. в статье [Знакомство с созданием надстроек SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins).
    
 
2. Откройте ASPX-файл, к которому требуется добавить веб-часть. В этой статье в качестве примера используется файл Default.aspx. 
    
 
3. Добавьте элемент **WebPartZone** в тот элемент **<asp:Content>**, в котором нужно указать веб-часть, используя часть кода, подобную приведенной ниже. Обычно его добавляют в тег **<asp:Content>**, где для свойства **ContentPlaceHolderId** задано значение `PlaceHolderMain`. Ниже приведен пример.
    
```XML
  <asp:Content ContentPlaceHolderId="PlaceHolderMain" runat="server">
  <WebPartPages:WebPartZone runat="server" FrameType="TitleBarOnly" 
      ID="HomePage1" Title="loc:full" />
</asp:Content>

```


     **Caution**  It is possible to add a Web Part element, such as  **<WebPartPages:XsltListViewWebPart>** as a child of the **WebPartZone**. But this is generally a bad practice in a SharePoint Add-in. If the add-in ever needs to be updated, a Web Part element inserted in the aspx file can cause the update to fail in some scenarios with the message "A web part with this ID has already been added to this page." We recommend that you add web parts to the elements manifest for the page as described later of this procedure.
4. Откройте файл манифеста элементов для страницы. Обычно это файл с именем elements.xml, размещенный в той же папке проекта, что и ASPX-файл.
    
 
5. В элементе **File** для страницы добавьте дочерний элемент **AllUsersWebPart** и задайте для его атрибута **WebPartZoneID** значение зоны веб-частей, созданной на странице. Ниже приведен пример.
    
```
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
    
```
  <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">
  <![CDATA[
    <webParts>

    </webParts>
  ]]>
</AllUsersWebPart>
```

7. Добавьте часть кода, заключенную в тег **webPart**, как дочерний объект элемента **webParts**. Ниже приведен пример добавления **XsltListViewWebPart**. Предполагается, что настраиваемый список с именем Test List входит в состав того же проекта надстройки. Дополнительные сведения о добавлении настраиваемого списка на сайт надстройки см. в статье [Создание надстроек с размещением у поставщика, которые включают пользовательский список SharePoint и тип контента](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-content-type). 
    
     **Примечание.** Обратите внимание, что у веб-части нет свойства идентификатора. Явно указывать идентификатор веб-части рекомендуем только в двух случаях (когда это действительно необходимо): если веб-часть добавляется на вики-страницу SharePoint и при подключении нескольких веб-частей.

```
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
    
 

