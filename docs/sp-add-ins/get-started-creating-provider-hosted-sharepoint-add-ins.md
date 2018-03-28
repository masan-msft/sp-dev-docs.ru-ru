---
title: Знакомство с созданием надстроек SharePoint с размещением у поставщика
description: Узнайте, как настроить среду разработки и создать свою первую надстройку SharePoint, размещаемую у поставщика.
ms.date: 03/14/2018
ms.prod: sharepoint
ms.openlocfilehash: 253dd72140a19e86d8a7d9d483dc289d0b022467
ms.sourcegitcommit: ad9b18a3fc81d9561383413644120e7255d31d61
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2018
---
# <a name="get-started-creating-provider-hosted-sharepoint-add-ins"></a>Создание надстроек SharePoint, размещаемых у поставщика

Надстройки, размещаемые у поставщика, — это один из двух основных типов надстроек SharePoint. Обзор надстроек SharePoint и этих основных типов см. в статье [Надстройки SharePoint](sharepoint-add-ins.md). 

Ниже представлен обзор надстроек, размещаемых у поставщика.

- К ним относятся веб-приложения, службы или базы данных, которые размещены на компьютерах, не относящихся к ферме SharePoint или подписке на SharePoint Online. Они также могут содержать компоненты SharePoint. Вы можете размещать внешние компоненты в любом стеке веб-хостинга, включая стек LAMP (Linux, Apache, MySQL и PHP).
- Пользовательская бизнес-логика надстройки должна запускаться на внешних компонентах или в JavaScript пользовательских страниц SharePoint.

В этой статье описаны следующие действия:

- Настройка среды разработки
- Создание проекта надстройки
- Написание кода надстройки

<a name="Setup"> </a>

## <a name="set-up-your-dev-environment"></a>Настройка среды разработки

Настроить среду для разработки надстроек SharePoint можно разными способами. Здесь описан самый простой из них. Информацию о настройке локальной среды и других альтернативных способах см. в [этой статье](tools-and-environments-for-developing-sharepoint-add-ins.md).

### <a name="get-the-tools"></a>Установите инструменты

- Если вы еще не установили **Visual Studio** 2013 или более поздней версии, сделайте это, следуя инструкциям из статьи [Установка Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio). Рекомендуем использовать [последнюю версию из Центра загрузки Майкрософт](https://www.visualstudio.com/downloads/download-visual-studio-vs).
 
- Visual Studio включает **Инструменты разработчика Microsoft Office для Visual Studio**. Иногда выпуск новой версии этих инструментов не совпадает с выходом обновлений Visual Studio. Чтобы убедиться, что у вас установлена последняя версия этих инструментов, запустите [установщик набора "Инструменты разработчика Office для Visual Studio 2013"](http://aka.ms/OfficeDevToolsForVS2013) или [установщик набора "Инструменты разработчика Office для Visual Studio 2015"](http://aka.ms/OfficeDevToolsForVS2015). 

Сверяйтесь с [более ранними версиями Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx) или другой [документацией по Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/).

<a name="o365_signup"> </a>

### <a name="sign-up-for-an-office-365-developer-subscription"></a>Получение подписки разработчика Office 365

> [!NOTE]
> Возможно, у вас уже есть доступ к подписке разработчика Office 365: 
> - **Вы подписчик Visual Studio (MSDN)?** Подписчики Visual Studio Ultimate и Visual Studio Premium с MSDN получают подписку разработчика Office 365 бесплатно. [Воспользуйтесь этим преимуществом сегодня](https://msdn.microsoft.com/subscriptions/manage/default.aspx). 
> - **У вас есть один из указанных ниже планов подписки на Office 365?** [Создайте сайт разработчика, используя имеющуюся подписку на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md). 

Чтобы получить план Office 365: 

- [Зарегистрируйтесь в программе для разработчиков Office 365](https://developer.microsoft.com/ru-RU/office/dev-program).

- Пошаговые инструкции для принятия участия в этой программе, регистрации и настройки подписки см. в [документации по программе для разработчиков приложений для Office 365](https://docs.microsoft.com/ru-RU/office/developer-program/office-365-developer-program).

### <a name="open-your-developer-site"></a>Открытие сайта разработчика 
 
Перейдите по ссылке **Создание надстроек** в левом верхнем углу страницы, чтобы открыть сайт разработчика. Открывшийся сайт должен выглядеть так, как показано на следующем рисунке. Наличие на странице списка **Тестируемые надстройки** подтверждает, что веб-сайт был создан с помощью шаблона "Сайт разработчика" SharePoint. Если вместо этого отображается обычный сайт группы, подождите несколько минут и перезагрузите сайт.
    
> [!NOTE]
> Запишите URL-адрес сайта. Он используется при создании проектов надстроек SharePoint в Visual Studio.
    
**Домашняя страница сайта разработчика со списком "Тестируемые надстройки"**

![Снимок экрана: домашняя страница сайта разработчика.](../images/SP15_DeveloperSiteHome_border.png)
 
<a name="Create"> </a>

## <a name="create-the-add-in-project"></a>Создание проекта надстройки

1. Запустите Visual Studio, выбрав команду **Запуск от имени администратора**.
    
2. В Visual Studio выберите **Файл** > **Создать** > **Проект**.
    
3. В диалоговом окне **Создание проекта** последовательно разверните узлы **Visual C#** и **Office/SharePoint**, а затем выберите **Надстройки** > **Надстройка SharePoint**.
    
4. Назовите проект **SampleAddIn** и нажмите кнопку **ОК**.
   
5. В диалоговом окне **Укажите параметры надстройки SharePoint** выполните указанные ниже действия.
    
   - Укажите полный URL-адрес сайта SharePoint, который вы хотите использовать для отладки надстройки. Это URL-адрес сайта разработчика. В URL-адресе используйте протокол HTTPS, а не HTTP. В какой-то момент выполнения этой процедуры или вскоре после его завершения вам будет предложено войти на сайт. Это не всегда происходит в одно и то же время. Используйте учетные данные администратора (в домене \*.onmicrosoft.com), созданные при регистрации сайта разработчика (например, Moye_Imya@contoso.onmicrosoft.com).    

   - В разделе **Как требуется разместить надстройку SharePoint?** выберите элемент **Размещено у поставщика**.

   - Нажмите кнопку **Далее**.  
 
6. На странице **Указание целевой версии SharePoint** выберите **SharePoint Online**, а затем нажмите кнопку **Далее**.

7. В разделе **Какой тип проекта веб-приложения требуется создать?** выберите пункт **Приложение веб-форм ASP.NET**, а затем нажмите кнопку **Далее**.

8. В разделе **Как требуется выполнять проверку подлинности надстройки?** выберите пункт **Использовать службу контроля доступа Microsoft Azure**.

9. В мастере нажмите кнопку **Готово**.
    
   Основная часть операций по настройке совершается при открытии решения. В решении Visual Studio создаются два проекта: один для надстройки SharePoint, а другой — для веб-приложения ASP.NET.

<a name="Code"> </a>
## <a name="code-your-add-in"></a>Написание кода надстройки

1. Откройте файл AppManifest.xml. На вкладке **Разрешения** укажите область **Коллекция сайтов** и уровень разрешений **Read**.

2. Удалите разметку в теге `<body>` файла Pages/Default.aspx веб-приложения, а затем добавьте приведенные ниже элементы управления HTML и ASP.NET в `<body>`. В этом примере используется элемент управления [UpdatePanel](http://msdn2.microsoft.com/ru-RU/library/bb359258) для обеспечения частичной отрисовки страницы.
    
    ```HTML
     <form id="form1" runat="server">
       <div>
         <asp:ScriptManager ID="ScriptManager1" runat="server"
                 EnablePartialRendering="true" />
         <asp:UpdatePanel ID="PopulateData" runat="server" UpdateMode="Conditional">
           <ContentTemplate>      
             <table border="1" cellpadding="10">
              <tr><th><asp:LinkButton ID="CSOM" runat="server" Text="Populate Data" 
                                    OnClick="CSOM_Click" /></th></tr>
              <tr><td>

             <h2>SharePoint Site</h2>
             <asp:Label runat="server" ID="WebTitleLabel"/>

             <h2>Current User:</h2>
             <asp:Label runat="server" ID="CurrentUserLabel" />

             <h2>Site Users</h2>
             <asp:ListView ID="UserList" runat="server">     
                 <ItemTemplate >
                   <asp:Label ID="UserItem" runat="server" 
                                     Text="<%# Container.DataItem.ToString()  %>">
                   </asp:Label><br />
                </ItemTemplate>
             </asp:ListView>

             <h2>Site Lists</h2>
                    <asp:ListView ID="ListList" runat="server">
                        <ItemTemplate >
                          <asp:Label ID="ListItem" runat="server" 
                                     Text="<%# Container.DataItem.ToString()  %>">
                         </asp:Label><br />
                       </ItemTemplate>
                   </asp:ListView>
                 </td>              
               </tr>
              </table>
            </ContentTemplate>
          </asp:UpdatePanel>
       </div>
     </form>
    ```

3. Добавьте приведенные ниже объявления в файл Default.aspx.cs веб-приложения.
    
    ```C#
       using Microsoft.SharePoint.Client;
       using Microsoft.IdentityModel.S2S.Tokens;
       using System.Net;
       using System.IO;
       using System.Xml;
    ```

4. В файле Default.aspx.cs веб-приложения добавьте указанные ниже переменные в класс [Page](http://msdn2.microsoft.com/ru-RU/library/dfbt9et1).
    
   ```C#
     SharePointContextToken contextToken;
     string accessToken;
     Uri sharepointUrl;
     string siteName;
     string currentUser;
     List<string> listOfUsers = new List<string>();
     List<string> listOfLists = new List<string>();
   ```

5. Добавьте метод `RetrieveWithCSOM` в класс [Page](http://msdn2.microsoft.com/ru-RU/library/dfbt9et1). Этот метод использует CSOM SharePoint, чтобы получать сведения о вашем сайте и отображать их на странице.
    
    ```C#
        // This method retrieves information about the host web by using the CSOM.
      private void RetrieveWithCSOM(string accessToken)
      {

          if (IsPostBack)
          {
              sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);
          }            

          ClientContext clientContext =
                          TokenHelper.GetClientContextWithAccessToken(
                              sharepointUrl.ToString(), accessToken);

          // Load the properties for the web object.
          Web web = clientContext.Web;
          clientContext.Load(web);
          clientContext.ExecuteQuery();

          // Get the site name.
          siteName = web.Title;

          // Get the current user.
          clientContext.Load(web.CurrentUser);
          clientContext.ExecuteQuery();
          currentUser = clientContext.Web.CurrentUser.LoginName;

          // Load the lists from the Web object.
          ListCollection lists = web.Lists;
          clientContext.Load<ListCollection>(lists);
          clientContext.ExecuteQuery();

          // Load the current users from the Web object.
          UserCollection users = web.SiteUsers;
          clientContext.Load<UserCollection>(users);
          clientContext.ExecuteQuery();

          foreach (User siteUser in users)
          {
              listOfUsers.Add(siteUser.LoginName);
          }

          foreach (List list in lists)
          {
              listOfLists.Add(list.Title);
          }
      }
    ```

6. Добавьте метод `CSOM_Click` в класс [Page](http://msdn2.microsoft.com/ru-RU/library/dfbt9et1). Этот метод вызывает событие, которое происходит, когда пользователь переходит по ссылке **Заполнение данными**.
    
    ```C#
      protected void CSOM_Click(object sender, EventArgs e)
    {
        string commandAccessToken = ((LinkButton)sender).CommandArgument;
        RetrieveWithCSOM(commandAccessToken);
        WebTitleLabel.Text = siteName;
        CurrentUserLabel.Text = currentUser;
        UserList.DataSource = listOfUsers;
        UserList.DataBind();
        ListList.DataSource = listOfLists;
        ListList.DataBind();    
     }
    ```

7. Замените существующий метод `Page_Load` указанным ниже. Метод `Page_Load` использует методы файла TokenHelper.cs, чтобы извлечь контекст из объекта `Request` и получить маркер доступа от службы контроля доступа Microsoft Azure (ACS).
    
    ```C#
      // The Page_load method fetches the context token and the access token. 
    // The access token is used by all of the data retrieval methods.
    protected void Page_Load(object sender, EventArgs e)
    {
         string contextTokenString = TokenHelper.GetContextTokenFromRequest(Request);

        if (contextTokenString != null)
        {
            contextToken =
                TokenHelper.ReadAndValidateContextToken(contextTokenString, Request.Url.Authority);

            sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);
            accessToken =
                        TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority)
                        .AccessToken;

             // For simplicity, this sample assigns the access token to the button's CommandArgument property. 
             // In a production add-in, this would not be secure. The access token should be cached on the server-side.
            CSOM.CommandArgument = accessToken;
        }
        else if (!IsPostBack)
        {
            Response.Write("Could not find a context token.");
            return;
        }
    }
    ```

8. После этого файл Default.aspx.cs должен выглядеть, как показано ниже.
    
    ```C#
      using System;
      using System.Collections.Generic;
      using System.Linq;
      using System.Web;
      using System.Web.UI;
      using System.Web.UI.WebControls;

      using Microsoft.SharePoint.Client;
      using Microsoft.IdentityModel.S2S.Tokens;
      using System.Net;
      using System.IO;
      using System.Xml;

      namespace SampleAddInWeb
      {
          public partial class Default : System.Web.UI.Page
          {
              SharePointContextToken contextToken;
              string accessToken;
              Uri sharepointUrl;
              string siteName;
              string currentUser;
              List<string> listOfUsers = new List<string>();
              List<string> listOfLists = new List<string>();

              protected void Page_PreInit(object sender, EventArgs e)
              {
                  Uri redirectUrl;
                  switch (SharePointContextProvider.CheckRedirectionStatus(Context, out redirectUrl))
                  {
                      case RedirectionStatus.Ok:
                          return;
                      case RedirectionStatus.ShouldRedirect:
                          Response.Redirect(redirectUrl.AbsoluteUri, endResponse: true);
                          break;
                      case RedirectionStatus.CanNotRedirect:
                          Response.Write("An error occurred while processing your request.");
                          Response.End();
                          break;
                  }
              }

              protected void CSOM_Click(object sender, EventArgs e)
              {
                  string commandAccessToken = ((LinkButton)sender).CommandArgument;
                  RetrieveWithCSOM(commandAccessToken);
                  WebTitleLabel.Text = siteName;
                  CurrentUserLabel.Text = currentUser;
                  UserList.DataSource = listOfUsers;
                  UserList.DataBind();
                  ListList.DataSource = listOfLists;
                  ListList.DataBind();
              }

              // This method retrieves information about the host web by using the CSOM.
              private void RetrieveWithCSOM(string accessToken)
              {

                  if (IsPostBack)
                  {
                      sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);
                  }

                  ClientContext clientContext =
                          TokenHelper.GetClientContextWithAccessToken(
                              sharepointUrl.ToString(), accessToken);

                  // Load the properties for the web object.
                  Web web = clientContext.Web;
                  clientContext.Load(web);
                  clientContext.ExecuteQuery();

                  // Get the site name.
                  siteName = web.Title;

                  // Get the current user.
                  clientContext.Load(web.CurrentUser);
                  clientContext.ExecuteQuery();
                  currentUser = clientContext.Web.CurrentUser.LoginName;

                  // Load the lists from the Web object.
                  ListCollection lists = web.Lists;
                  clientContext.Load<ListCollection>(lists);
                  clientContext.ExecuteQuery();

                  // Load the current users from the Web object.
                  UserCollection users = web.SiteUsers;
                  clientContext.Load<UserCollection>(users);
                  clientContext.ExecuteQuery();

                  foreach (User siteUser in users)
                  {
                      listOfUsers.Add(siteUser.LoginName);
                  }

                  foreach (List list in lists)
                  {
                      listOfLists.Add(list.Title);
                  }
              }

              protected void Page_Load(object sender, EventArgs e)
              {
                  string contextTokenString = 
                       TokenHelper.GetContextTokenFromRequest(Request);

                  if (contextTokenString != null)
                  {
                      contextToken =
                          TokenHelper.ReadAndValidateContextToken(contextTokenString, Request.Url.Authority);

                      sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);
                      accessToken =
                          TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority)
                                     .AccessToken;
                      CSOM.CommandArgument = accessToken;
                  }
                  else if (!IsPostBack)
                  {
                      Response.Write("Could not find a context token.");
                      return;
                  }
              }
          }
      }
     
    ```

9. Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Если отобразится окно **Оповещение системы безопасности** с предложением доверять самозаверяющему сертификату Localhost, нажмите кнопку **Да**.
    
10. Выберите **Сделать доверенным** на странице подтверждения, чтобы предоставить надстройке разрешения. Visual Studio установит веб-приложение в IIS Express, а затем установит надстройку на тестовом сайте SharePoint и запустит ее. Откроется страница с таблицей, как на приведенном ниже снимке экрана. Чтобы просмотреть сводную информацию о сайте SharePoint, выберите **Заполнение данных**.

   ![Страница запуска базовой надстройки с размещением у поставщика](../images/SP15_basicself-hostedapp.gif)
 

<a name="SP15createprovider_nextsteps"> </a>    
## <a name="next-steps"></a>Дальнейшие действия

Порядок дальнейших действий с надстройкой:
 
1.  [Настройка внешнего вида надстройки SharePoint с размещением у поставщика](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)
2.  [Добавление настраиваемой кнопки в надстройку, размещенную у поставщика](include-a-custom-button-in-the-provider-hosted-add-in.md)
3.  [Краткий обзор объектной модели SharePoint](get-a-quick-overview-of-the-sharepoint-object-model.md)
4.  [Добавление операций записи SharePoint в надстройку, размещенную у поставщика](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md)
5.  [Добавление веб-части надстройки в надстройку, размещенную у поставщика](include-an-add-in-part-in-the-provider-hosted-add-in.md)
6.  [Обработка событий надстройки, размещенной у поставщика](handle-add-in-events-in-the-provider-hosted-add-in.md)
7.  [Добавление логики, выполняемой при первом запуске, в надстройку, размещаемую у поставщика](add-first-run-logic-to-the-provider-hosted-add-in.md)
8.  [Программное развертывание собственной кнопки в надстройке с размещением у поставщика](programmatically-deploy-a-custom-button-in-the-provider-hosted-add-in.md)
9.  [Обработка событий элементов списков в надстройке с размещением у поставщика](handle-list-item-events-in-the-provider-hosted-add-in.md)




