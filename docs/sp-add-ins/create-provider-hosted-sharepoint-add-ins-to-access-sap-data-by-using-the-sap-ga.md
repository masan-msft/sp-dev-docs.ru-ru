---
title: Создание надстроек SharePoint, размещаемых у поставщика, для доступа к данным SAP
description: Узнайте, как создать надстройку SharePoint для получения авторизованного доступа к SAP с помощью шлюза SAP для Майкрософт.
ms.date: 12/27/2017
ms.prod: sharepoint
ms.openlocfilehash: da76de20f1e72d88d467c400d71fd03a279d7c31
ms.sourcegitcommit: 6bc4c8e43c260deabc60d41d633586bfa3e6024a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/28/2017
---
# <a name="create-provider-hosted-sharepoint-add-ins-to-access-sap-data-by-using-the-sap-gateway-for-microsoft"></a><span data-ttu-id="5f989-103">Создание надстроек SharePoint, размещаемых у поставщика, для доступа к данным SAP с помощью шлюза SAP для Майкрософт</span><span class="sxs-lookup"><span data-stu-id="5f989-103">Create provider-hosted SharePoint Add-ins to access SAP data by using the SAP Gateway for Microsoft</span></span>

<span data-ttu-id="5f989-104">Вы можете создать надстройку SharePoint, которая считывает и записывает данные SAP, а при необходимости и данные SharePoint, с помощью шлюза SAP для Майкрософт и библиотеки аутентификации Azure Active Directory для .NET.</span><span class="sxs-lookup"><span data-stu-id="5f989-104">You can create a SharePoint Add-in that reads and writes SAP data, and optionally reads and writes SharePoint data, by using SAP Gateway for Microsoft and the Azure AD Authentication Library for .NET. This article provides the procedures for how you can design the SharePoint Add-in to get authorized access to SAP.</span></span> <span data-ttu-id="5f989-105">В этой статье описано, как создать надстройку SharePoint для получения авторизованного доступа к SAP.</span><span class="sxs-lookup"><span data-stu-id="5f989-105">This article provides the procedures for how you can design the SharePoint Add-in to get authorized access to SAP.</span></span> 
 

## <a name="prerequisites"></a><span data-ttu-id="5f989-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5f989-106">Prerequisites</span></span>

<span data-ttu-id="5f989-107">Ниже перечислены компоненты, необходимые для выполнения процедур, описанных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5f989-107">The following are prerequisites to the procedures in this article:</span></span>

- <span data-ttu-id="5f989-108">**Сайт разработчика Office 365** в домене Office 365, связанном с подпиской Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5f989-108">An Office 365 Developer Site in an Office 365 domain that is associated with a Microsoft Azure Active Directory tenancy. See Sign up for an Office 365 Developer Site or Create a developer site on an existing Office 365 subscription.</span></span> <span data-ttu-id="5f989-109">См. статью [Настройка среды разработки надстроек SharePoint в Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md) или [Создание сайта разработчика с использованием имеющейся подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="5f989-109">An Office 365 Developer Site in an Office 365 domain that is associated with a Microsoft Azure Active Directory subscription. See [Set up a development environment for SharePoint Add-ins on Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md) or [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span>
    
- <span data-ttu-id="5f989-110">Приложение **Visual Studio 2013 c обновлением 2** или более поздней версии, которое вы можете получить на веб-странице [Вас приветствует Visual Studio](https://msdn.microsoft.com/library/dd831853.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f989-110">**Visual Studio 2013 Update 2** or later, which you can obtain from [Welcome to Visual Studio 2013](https://msdn.microsoft.com/library/dd831853.aspx).</span></span>

- <span data-ttu-id="5f989-p103">**Инструменты разработчика Microsoft Office для Visual Studio**. Версия, включенная в обновление 2 для Visual Studio 2013 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5f989-p103">**Microsoft Office Developer Tools for Visual Studio**. The version that is included in Update 2 of Visual Studio 2013 or later.</span></span>
    
- <span data-ttu-id="5f989-113">**Шлюз SAP Gateway для Майкрософт**, развернутый и настроенный в Azure.</span><span class="sxs-lookup"><span data-stu-id="5f989-113">**SAP Gateway for Microsoft** is deployed and configured in Microsoft Azure. See the documentation for SAP Gateway for Microsoft.</span></span> <span data-ttu-id="5f989-114">См. документацию по [шлюзу SAP для Майкрософт](https://help.sap.com/saphelp_nwgwpam_1/helpdata/en/b5/74d3ad2f33428193a32c09c351e0b3/frameset.htm).</span><span class="sxs-lookup"><span data-stu-id="5f989-114">A SAP OData endpoint with sample data in it. See the documentation for [SAP Gateway for Microsoft](https://help.sap.com/saphelp_nwgwpam_1/helpdata/en/b5/74d3ad2f33428193a32c09c351e0b3/frameset.htm).</span></span>
    
- <span data-ttu-id="5f989-115">**Учетная запись организации в Azure**.</span><span class="sxs-lookup"><span data-stu-id="5f989-115">**An organizational account in Azure**.</span></span> <span data-ttu-id="5f989-116">См. статью [Регистрация приложения API Office 365 в Azure AD](https://github.com/jasonjoh/office365-azure-guides/blob/master/RegisterAnAppInAzure.md).</span><span class="sxs-lookup"><span data-stu-id="5f989-116">See [Manually register an Office 365 API app in Azure AD](https://github.com/jasonjoh/office365-azure-guides/blob/master/RegisterAnAppInAzure.md).</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="5f989-117">После создания учетной записи Office 365 (login.microsoftonline.com) войдите в нее и измените временный пароль.</span><span class="sxs-lookup"><span data-stu-id="5f989-117">Log in to your Office 365 account (login.microsoftonline.com) to change the temporary password after the account is created.</span></span>

- <span data-ttu-id="5f989-p106">**Конечная точка OData для SAP** с примером данных. См. документацию к [шлюзу SAP для Майкрософт](https://help.sap.com/saphelp_nwgwpam_1/helpdata/en/b5/74d3ad2f33428193a32c09c351e0b3/frameset.htm).</span><span class="sxs-lookup"><span data-stu-id="5f989-p106">**A SAP OData endpoint** with sample data in it. See the documentation for [SAP Gateway for Microsoft](https://help.sap.com/saphelp_nwgwpam_1/helpdata/en/b5/74d3ad2f33428193a32c09c351e0b3/frameset.htm).</span></span>
    
- <span data-ttu-id="5f989-120">**Общее представление об Azure AD.**</span><span class="sxs-lookup"><span data-stu-id="5f989-120">**A basic familiarity with Azure AD.** See Getting started with Azure AD.</span></span> <span data-ttu-id="5f989-121">См. статью [Начало работы с Azure AD](https://docs.microsoft.com/ru-RU/azure/active-directory/get-started-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="5f989-121">See [Get started with Azure AD](https://docs.microsoft.com/ru-RU/azure/active-directory/get-started-azure-ad).</span></span>
    
- <span data-ttu-id="5f989-122">**Общее представление о надстройках SharePoint.** См. статью [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="5f989-122">**A basic familiarity with creating SharePoint Add-ins.** See [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span></span>

- <span data-ttu-id="5f989-123">**Общее представление об OAuth 2.0 в Azure AD.**</span><span class="sxs-lookup"><span data-stu-id="5f989-123">A basic familiarity with OAuth 2.0 in Azure AD. See OAuth 2.0 and in Azure AD and its child topics.</span></span> <span data-ttu-id="5f989-124">См. статью [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](https://docs.microsoft.com/ru-RU/azure/active-directory/develop/active-directory-protocols-oauth-code) и связанные с ней статьи.</span><span class="sxs-lookup"><span data-stu-id="5f989-124">See [Authorize access to web applications using OAuth 2.0 and Azure Active Directory](https://docs.microsoft.com/ru-RU/azure/active-directory/develop/active-directory-protocols-oauth-code) and its child topics.</span></span>
    
- <span data-ttu-id="5f989-125">**Пример кода.** [SharePoint: использование шлюза SAP для Майкрософт в надстройке SharePoint](https://code.msdn.microsoft.com/office/sharepoint-2013-using-the-0931abce)</span><span class="sxs-lookup"><span data-stu-id="5f989-125">**Code sample:** [SharePoint: Using the SAP Gateway to Microsoft in a SharePoint Add-in](https://code.msdn.microsoft.com/office/sharepoint-2013-using-the-0931abce)</span></span>
 

<span data-ttu-id="5f989-126"><a name="AuthOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="5f989-126"></span></span> 

## <a name="understand-authentication-and-authorization-to-sap-gateway-for-microsoft-and-sharepoint"></a><span data-ttu-id="5f989-127">Общие сведения о проверке подлинности и авторизации в шлюзе SAP для Майкрософт и SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f989-127">Understand authentication and authorization to SAP Gateway for Microsoft and SharePoint</span></span>

<span data-ttu-id="5f989-128">С помощью OAuth 2.0 в Azure AD приложения могут получать доступ к нескольким ресурсам, размещаемым в Azure. В их число входит шлюз SAP для Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5f989-128">OAuth 2.0 in Azure AD enables applications to access multiple resources hosted by Azure, and SAP Gateway for Microsoft is one of them.</span></span> <span data-ttu-id="5f989-129">В протоколе OAuth 2.0 субъектами безопасности являются не только пользователи, но и приложения.</span><span class="sxs-lookup"><span data-stu-id="5f989-129">With OAuth 2.0, applications, in addition to users, are security principals.</span></span> <span data-ttu-id="5f989-130">Субъектам приложений необходимы проверка подлинности и авторизация для защищенных ресурсов, а не только для пользователей (а иногда и вместо них).</span><span class="sxs-lookup"><span data-stu-id="5f989-130">Application principals require authentication and authorization to protected resources in addition to (and sometimes instead of) users.</span></span> 

<span data-ttu-id="5f989-p110">В этом процессе участвует поток OAuth, в котором приложение (например, надстройка SharePoint) получает маркеры доступа и обновления. Маркер доступа принимают все службы и приложения, размещенные в Azure и использующие Azure AD в качестве сервера авторизации OAuth 2.0. Этот процесс во многом аналогичен тому, как удаленные компоненты надстройки SharePoint, размещенной у поставщика, получают авторизацию для SharePoint (см. статью [Создание надстроек для SharePoint, использующих авторизацию с низким уровнем доверия](creating-sharepoint-add-ins-that-use-low-trust-authorization.md) и ее подразделы). Однако система авторизации для контроля доступа использует в качестве доверенного поставщика маркеров службу контроля доступа Azure (ACS), а не Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f989-p110">OAuth 2.0 in Azure AD enables applications to access multiple resources hosted by Microsoft Azure and SAP Gateway for Microsoft is one of them. With OAuth 2.0, applications, in addition to users, are security principals. Application principals require authentication and authorization to protected resources in addition to (and sometimes instead of) users. The process involves an OAuth "flow" in which the application, which can be a SharePoint Add-in, obtains an access token (and refresh token) that is accepted by all of the Microsoft Azure-hosted services and applications that are configured to use Azure AD as an OAuth 2.0 authorization server. The process is very similar to the way that the remote components of a provider-hosted SharePoint Add-in gets authorization to SharePoint as described in  [Creating SharePoint Add-ins that use low-trust authorization](creating-sharepoint-add-ins-that-use-low-trust-authorization.md) and its child articles. However, the ACS authorization system uses Microsoft Azure Access Control Service (ACS) as the trusted token issuer rather than Azure AD.</span></span>
 
> [!TIP] 
> <span data-ttu-id="5f989-134">Если надстройка SharePoint получает доступ не только к шлюзу SAP для Майкрософт, но и к SharePoint, то она должна использовать *обе* системы: Azure AD для получения маркера доступа к шлюзу SAP для Майкрософт и систему авторизации ACS для получения маркера доступа к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f989-134">Tip  If your SharePoint Add-in accesses SharePoint in addition to accessing SAP Gateway for Microsoft, then it will need to use  *both*  systems: Azure AD to get an access token to SAP Gateway for Microsoft and the ACS authorization system to get an access token to SharePoint. The tokens from the two sources are not interchangeable. For more information, see Optionally, add SharePoint access to the ASP.NET application.</span></span> <span data-ttu-id="5f989-135">Маркеры из этих двух источников не являются взаимозаменяемыми.</span><span class="sxs-lookup"><span data-stu-id="5f989-135">The tokens from the two sources are not interchangeable.</span></span> <span data-ttu-id="5f989-136">Дополнительные сведения см. в разделе [Предоставление приложению ASP.NET доступа к SharePoint (необязательно)](#SharePoint).</span><span class="sxs-lookup"><span data-stu-id="5f989-136">For more information, see [Add SharePoint access to the ASP.NET application (optional)](#SharePoint).</span></span>

<span data-ttu-id="5f989-137">Подробное описание и схему потока OAuth, используемого протоколом OAuth 2.0 в Azure AD, см. в статье [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](https://docs.microsoft.com/ru-RU/azure/active-directory/develop/active-directory-protocols-oauth-code).</span><span class="sxs-lookup"><span data-stu-id="5f989-137">For a detailed description and diagram of the OAuth flow used by OAuth 2.0 in Azure AD, see [Authorize access to web applications using OAuth 2.0 and Azure Active Directory](https://docs.microsoft.com/ru-RU/azure/active-directory/develop/active-directory-protocols-oauth-code).</span></span> 

<span data-ttu-id="5f989-138">Подобное описание и схему потока для доступа к SharePoint см. в [руководстве по потоку токена контекста](context-token-oauth-flow-for-sharepoint-add-ins.md#OAuth_ProcessFlowSteps).</span><span class="sxs-lookup"><span data-stu-id="5f989-138">For a detailed description and diagram of the OAuth flow used by OAuth 2.0 in Azure AD, see  Authorization Code Grant Flow. (For a similar description, and a diagram, of the flow for accessing SharePoint, see  See the steps in the Context Token flow.)</span></span>


## <a name="create-the-sharepoint-add-in"></a><span data-ttu-id="5f989-139">Создание надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f989-139">Create the SharePoint Add-in</span></span>

### <a name="to-create-the-visual-studio-solution"></a><span data-ttu-id="5f989-140">Создание решения Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5f989-140">To create the Visual Studio solution</span></span>


1. <span data-ttu-id="5f989-141">Создайте проект **надстройки SharePoint** в Visual Studio, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5f989-141">Create a **SharePoint Add-in** project in Visual Studio with the following steps.</span></span> <span data-ttu-id="5f989-142">В примере из этой статьи используется язык C#, но вы также можете создать проект надстройки SharePoint с помощью раздела **Visual Basic** шаблонов нового проекта.</span><span class="sxs-lookup"><span data-stu-id="5f989-142">Create an  SharePoint Add-in project in Visual Studio with the following steps. (The continuing example in this article assumes you are using C#; but you can start a SharePoint Add-in project in the **Visual Basic** section of the new project templates as well.)</span></span>
    
  1. <span data-ttu-id="5f989-143">В мастере создания надстройки SharePoint введите имя проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5f989-143">In the  New SharePoint Add-in wizard, name the project and click OK. For the continuing example, use SAP2SharePoint.</span></span> <span data-ttu-id="5f989-144">Для нашего примера укажите имя **SAP2SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="5f989-144">For the continuing example, use **SAP2SharePoint**.</span></span>
      
  2. <span data-ttu-id="5f989-145">Укажите URL-адрес вашего сайта разработчика Office 365 (включая косую черту в конце) в качестве сайта отладки. Пример: `https://<O365_domain>.sharepoint.com/`.</span><span class="sxs-lookup"><span data-stu-id="5f989-145">Specify the domain URL of your Office 365 Developer Site (including a final forward slash) as the debugging site; for example, https://<O365_domain>.sharepoint.com/. Specify  Provider-hosted as the add-in type. Click Next`https://<O365_domain>.sharepoint.com/`.</span></span> <span data-ttu-id="5f989-146">Выберите тип надстройки **Размещение у поставщика** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="5f989-146">Specify **Provider-hosted** as the add-in type, and then select **Next**.</span></span>
      
  3. <span data-ttu-id="5f989-147">Выберите тип проекта.</span><span class="sxs-lookup"><span data-stu-id="5f989-147">Select a chart type.</span></span> <span data-ttu-id="5f989-148">Для нашего примера выберите **Приложение веб-форм ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="5f989-148">For the continuing example, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="5f989-149">Вы также можете создавать приложения ASP.NET MVC, получающие доступ к шлюзу SAP для Майкрософт. Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="5f989-149">Choose a project type. For the continuing example, choose  ASP.NET Web Forms Application. (You can also make ASP.NET MVC applications that access SAP Gateway for Microsoft.) Click  **Next**.</span></span>
      
  4. <span data-ttu-id="5f989-150">Выберите Azure ACS в качестве системы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5f989-150">Select Azure ACS as the authentication system.</span></span> <span data-ttu-id="5f989-151">Надстройка SharePoint будет использовать эту систему для доступа к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f989-151">(Your SharePoint Add-in uses this system if it accesses SharePoint.</span></span> <span data-ttu-id="5f989-152">Эта система не используется при доступе к шлюзу SAP для Майкрософт. Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="5f989-152">It does not use this system when it accesses SAP Gateway for Microsoft.) Select **Finish**.</span></span>
 
2. <span data-ttu-id="5f989-153">После создания проекта вам будет предложено войти в учетную запись Office 365.</span><span class="sxs-lookup"><span data-stu-id="5f989-153">After the project is created, you are prompted to login to the Office 365 account. Use the credentials of an account administrator; for example Bob@<O365_domain>.onmicrosoft.com.</span></span> <span data-ttu-id="5f989-154">Используйте учетные данные администратора учетной записи, например `Bob@<O365_domain>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="5f989-154">Use the credentials of an account administrator; for example `Bob@<O365_domain>.onmicrosoft.com`.</span></span>
 
3. <span data-ttu-id="5f989-155">Решение Visual Studio включает два проекта: проект самой надстройки SharePoint и проект веб-форм ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5f989-155">There are two projects in the Visual Studio solution; the SharePoint Add-in proper project and an ASP.NET web forms project. Add the  Active Directory Authentication Library (ADAL) package to the ASP.NET project with these steps:</span></span> <span data-ttu-id="5f989-156">Добавьте пакет **библиотеки проверки подлинности Active Directory** (ADAL) к проекту ASP.NET, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5f989-156">Add the **Active Directory Authentication Library** (ADAL) package to the "Web" project with these steps:</span></span>
    
  1. <span data-ttu-id="5f989-157">Щелкните правой кнопкой мыши папку **Ссылки** проекта ASP.NET (в нашем примере он называется **SAP2SharePointWeb**) и выберите команду **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5f989-157">Right-click the  **References** folder in the ASP.NET project (named **SAP2SharePointWeb** in the continuing example) and select **Manage NuGet Packages**.</span></span> 
      
  2. <span data-ttu-id="5f989-158">В открывшемся диалоговом окне выберите **Сеть**.</span><span class="sxs-lookup"><span data-stu-id="5f989-158">In the dialog that opens, select  **Online** on the left. EnterMicrosoft.IdentityModel.Clients.ActiveDirectory in the search box.</span></span> <span data-ttu-id="5f989-159">Введите **Microsoft.IdentityModel.Clients.ActiveDirectory** в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="5f989-159">In the dialog that opens, select Online on the left. Enter **Microsoft.IdentityModel.Clients.ActiveDirectory** in the search box.</span></span>
      
  3. <span data-ttu-id="5f989-160">Когда в результатах поиска появится библиотека ADAL, нажмите кнопку **Установить** и примите условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="5f989-160">When the ADAL library appears in the search results, click the  **Install** button beside it, and accept the license when prompted.</span></span>
    
4. <span data-ttu-id="5f989-161">Добавьте пакет Json.net в проект ASP.NET, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5f989-161">Add the Json.net package to the ASP.NET project with these steps:</span></span>
    
  1. <span data-ttu-id="5f989-162">Введите **Json.net** в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="5f989-162">Enter **Json.net** in the search box.</span></span> <span data-ttu-id="5f989-163">Если появится слишком много результатов, попробуйте выполнить поиск по запросу **Newtonsoft.json**.</span><span class="sxs-lookup"><span data-stu-id="5f989-163">Enter **Json.net** in the search box. If this produces too many hits, try searching on Newtonsoft.json.</span></span>
      
  2. <span data-ttu-id="5f989-164">Когда в результатах поиска появится библиотека Json.net, нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="5f989-164">When Json.net appears in the search results, click the  **Install** button beside it.</span></span>
 
5. <span data-ttu-id="5f989-165">Нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="5f989-165">Select **Save and Close**.</span></span>
    

### <a name="to-register-your-web-application-with-azure-ad"></a><span data-ttu-id="5f989-166">Регистрация веб-приложения в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f989-166">Register your web application with Azure AD</span></span>

1. <span data-ttu-id="5f989-167">Войдите на [портал управления Azure](https://manage.windowsazure.com), используя учетную запись администратора Azure.</span><span class="sxs-lookup"><span data-stu-id="5f989-167">Login into the  [Azure Management portal](https://manage.windowsazure.com) with your Azure administrator account.</span></span>
    
  > [!NOTE] 
  > <span data-ttu-id="5f989-168">Из соображений безопасности не рекомендуем использовать учетную запись администратора при разработке надстроек.</span><span class="sxs-lookup"><span data-stu-id="5f989-168">Note  For security purposes, we recommend against using an administrator account when developing add-ins.</span></span>

2. <span data-ttu-id="5f989-169">Выберите **Active Directory** в левой части страницы.</span><span class="sxs-lookup"><span data-stu-id="5f989-169">Choose  **Active Directory** on the left side.</span></span>    
 
3. <span data-ttu-id="5f989-170">Выберите каталог.</span><span class="sxs-lookup"><span data-stu-id="5f989-170">Select your directory.</span></span>     
 
4. <span data-ttu-id="5f989-171">Выберите **ПРИЛОЖЕНИЯ** (на верхней панели навигации).</span><span class="sxs-lookup"><span data-stu-id="5f989-171">Choose  **APPLICATIONS** (on the top navigation bar).</span></span>    
 
5. <span data-ttu-id="5f989-172">На панели инструментов в нижней части экрана нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5f989-172">Choose  **Add** on the toolbar at the bottom of the screen.</span></span>    
 
6. <span data-ttu-id="5f989-173">В открывшемся диалоговом окне выберите элемент **Добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="5f989-173">On the dialog that opens, choose  **Add an application my organization is developing**.</span></span>    
 
7. <span data-ttu-id="5f989-174">В диалоговом окне **ДОБАВЛЕНИЕ ПРИЛОЖЕНИЯ** введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="5f989-174">On the  **ADD APPLICATION** dialog, give the application a name. For the continuing example, useContosoAutomobileCollection.</span></span> <span data-ttu-id="5f989-175">Для нашего примера укажите имя **ContosoAutomobileCollection**.</span><span class="sxs-lookup"><span data-stu-id="5f989-175">For the continuing example, use **ContosoAutomobileCollection**.</span></span>     
 
8. <span data-ttu-id="5f989-176">Выберите тип надстройки **Веб-надстройка или веб-API** и нажмите кнопку со стрелкой вправо.</span><span class="sxs-lookup"><span data-stu-id="5f989-176">Choose  **Web Application And/Or Web API** as the application type, and then click the right arrow button.</span></span>    
 
9. <span data-ttu-id="5f989-177">На второй странице диалогового окна укажите в поле **URL-адрес для входа** URL-адрес отладки SSL из проекта ASP.NET решения Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f989-177">On the second page of the dialog, use the SSL debugging URL from the ASP.NET project in the Visual Studio solution as the **SIGN-ON URL**.</span></span> <span data-ttu-id="5f989-178">Чтобы узнать этот URL-адрес, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5f989-178">You can find the URL using the following steps.</span></span> <span data-ttu-id="5f989-179">*Сначала необходимо зарегистрировать надстройку с URL-адресом отладки, чтобы иметь возможность запускать отладчик Visual Studio (F5). Когда надстройка будет готова к размещению, вы повторно зарегистрируете ее, используя URL-адрес веб-сайта Azure. См. раздел [Изменение надстройки и ее размещение в Azure и Office 365](#Stage).*</span><span class="sxs-lookup"><span data-stu-id="5f989-179">On the second page of the dialog, use the SSL debugging URL from the ASP.NET project in the Visual Studio solution as the SIGN-ON URL. You can find the URL using the following steps. (You need to register the add-in initially with the debugging URL so that you can run the Visual Studio debugger (F5). When your add-in is ready for staging, you will re-register it with its staging Azure Web Site URL.  Modify the add-in and stage it to Azure and Office 365.)</span></span>
    
  1. <span data-ttu-id="5f989-180">Выделите проект ASP.NET в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="5f989-180">Highlight the ASP.NET project in **Solution Explorer**.</span></span> 

  2. <span data-ttu-id="5f989-181">В окне **Свойства** скопируйте значение свойства **URL-АДРЕС SSL**.</span><span class="sxs-lookup"><span data-stu-id="5f989-181">In the **Properties** window, copy the value of the **SSL URL** property. An example ishttps://localhost:44300/.</span></span> <span data-ttu-id="5f989-182">Пример: `https://localhost:44300/`.</span><span class="sxs-lookup"><span data-stu-id="5f989-182">An example is `https://localhost:44300/`.</span></span>
      
  3. <span data-ttu-id="5f989-183">Вставьте его в поле **URL-АДРЕС ДЛЯ ВХОДА** диалогового окна **ДОБАВЛЕНИЕ ПРИЛОЖЕНИЯ**.</span><span class="sxs-lookup"><span data-stu-id="5f989-183">Paste it into the **SIGN-ON URL** on the **ADD APPLICATION** dialog.</span></span>
    
10. <span data-ttu-id="5f989-184">В качестве **URI ИДЕНТИФИКАТОРА ПРИЛОЖЕНИЯ** укажите уникальный URI, например имя приложения, добавленное к URL-адресу SSL: `https://localhost:44300/ContosoAutomobileCollection`.</span><span class="sxs-lookup"><span data-stu-id="5f989-184">For the APP ID URI, give the application a unique URI, such as the application name appended to the end of the SSL URL; for example https://localhost:44300/ContosoAutomobileCollection.</span></span>    
 
11. <span data-ttu-id="5f989-185">Нажмите кнопку с галочкой.</span><span class="sxs-lookup"><span data-stu-id="5f989-185">Select the Submit button.</span></span> <span data-ttu-id="5f989-186">Откроется информационная панель Azure для приложения с сообщением об успешном выполнении операции.</span><span class="sxs-lookup"><span data-stu-id="5f989-186">Click the checkmark button. The Azure dashboard for the application opens with a success message.</span></span>    
 
12. <span data-ttu-id="5f989-187">Выберите пункт **НАСТРОЙКА** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5f989-187">Choose **CONFIGURE** on the top of the page.</span></span>    
 
13. <span data-ttu-id="5f989-p125">Найдите **КОД КЛИЕНТА** и скопируйте его. Он пригодится для дальнейших действий.</span><span class="sxs-lookup"><span data-stu-id="5f989-p125">Scroll to the **CLIENT ID** and make a copy of it. You will need it for a later procedure.</span></span>    
 
14. <span data-ttu-id="5f989-190">В разделе **Ключи** создайте ключ.</span><span class="sxs-lookup"><span data-stu-id="5f989-190">In the **keys** section, create a key.</span></span> <span data-ttu-id="5f989-191">Он появится не сразу.</span><span class="sxs-lookup"><span data-stu-id="5f989-191">It won't appear initially.</span></span> <span data-ttu-id="5f989-192">Нажмите кнопку **СОХРАНИТЬ** в нижней части страницы, и ключ станет виден.</span><span class="sxs-lookup"><span data-stu-id="5f989-192">Select **SAVE** at the bottom of the page and the key will be visible.</span></span> <span data-ttu-id="5f989-193">Скопируйте его.</span><span class="sxs-lookup"><span data-stu-id="5f989-193">Make a copy of corev15.css and name it contosov15.css.</span></span> <span data-ttu-id="5f989-194">Он понадобится вам позже.</span><span class="sxs-lookup"><span data-stu-id="5f989-194">Scroll to the  CLIENT ID and make a copy of it. You will need it for a later procedure.</span></span>    
 
15. <span data-ttu-id="5f989-195">Прокрутите вниз до раздела **Разрешения для других приложений** и выберите свое приложение-службу шлюза SAP для Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5f989-195">Scroll to  **permissions to other applications** and select your SAP Gateway for Microsoft service application.</span></span>    
 
16. <span data-ttu-id="5f989-196">Откройте раскрывающийся список **Делегированные разрешения** и выберите разрешения службы шлюза SAP для Майкрософт, которые будет использовать ваша надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f989-196">Open the  **Delegated Permissions** drop down list and enable the boxes for the permissions to the SAP Gateway for Microsoft service that your SharePoint Add-in will need.</span></span>    
 
17. <span data-ttu-id="5f989-197">Нажмите кнопку **СОХРАНИТЬ** в нижней части экрана.</span><span class="sxs-lookup"><span data-stu-id="5f989-197">Click  **SAVE** at the bottom of the screen.</span></span>
    
 

### <a name="to-configure-the-application-to-communicate-with-azure-ad"></a><span data-ttu-id="5f989-198">Настройка приложения для взаимодействия с Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f989-198">Configure the application to communicate with Azure AD</span></span>

1. <span data-ttu-id="5f989-199">В Visual Studio откройте файл web.config проекта ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5f989-199">In Visual Studio, open the web.config file in the ASP.NET project.</span></span>    
 
2. <span data-ttu-id="5f989-200">В разделе `<appSettings>` в Инструментах разработчика Office для Visual Studio появились элементы **ClientID** и **ClientSecret** надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f989-200">In the `<appSettings>` section, the Office Developer Tools for Visual Studio have added elements for the **ClientID** and **ClientSecret** of the SharePoint Add-in.</span></span> <span data-ttu-id="5f989-201">Они используются в системе авторизации Azure ACS, если приложение ASP.NET получает доступ к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f989-201">(These are used in the Azure ACS authorization system if the ASP.NET application accesses SharePoint.</span></span> <span data-ttu-id="5f989-202">В нашем примере можно не обращать на них внимания, но не следует удалять их.</span><span class="sxs-lookup"><span data-stu-id="5f989-202">You can ignore them for the continuing example, but do not delete them.</span></span> <span data-ttu-id="5f989-203">Они необходимы в надстройках SharePoint, размещаемых у поставщика, даже если надстройка не получает доступ к данным SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f989-203">They are required in provider-hosted SharePoint Add-ins even if the add-in is not accessing SharePoint data.</span></span> <span data-ttu-id="5f989-204">Их значения меняются при каждом нажатии клавиши F5 в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f989-204">Their values change each time you select F5 in Visual Studio.)</span></span> 

  <span data-ttu-id="5f989-205">Добавьте в раздел два приведенных ниже элемента.</span><span class="sxs-lookup"><span data-stu-id="5f989-205">Add the following two elements to the section.</span></span> <span data-ttu-id="5f989-206">Приложение использует их для проверки подлинности в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f989-206">These are used by the application to authenticate to Azure AD.</span></span> <span data-ttu-id="5f989-207">Помните, что приложения, как и пользователи, являются субъектами безопасности в системах с проверкой подлинности и авторизацией на основе OAuth.</span><span class="sxs-lookup"><span data-stu-id="5f989-207">(Remember that applications, as well as users, are security principals in OAuth-based authentication and authorization systems.)</span></span>
      
  ```
    <add key="ida:ClientID" value="" />
    <add key="ida:ClientKey" value="" />
  ```

3. <span data-ttu-id="5f989-208">Вставьте сохраненный ранее идентификатор клиента из каталога Azure AD в качестве значения ключа **ida:ClientID**.</span><span class="sxs-lookup"><span data-stu-id="5f989-208">Insert the Client ID that you saved from your Azure AD directory in the earlier procedure as the value of the **ida:ClientID** key.</span></span> <span data-ttu-id="5f989-209">Оставьте регистр и пунктуацию без изменений. Будьте внимательны, чтобы не добавить пробел в начале или конце значения.</span><span class="sxs-lookup"><span data-stu-id="5f989-209">In the <appSettings> section, insert the client ID that you saved from the winazureadshort registration process as the value of the ida:ClientID key. Leave the casing and punctuation exactly as you copied it and be careful not to include a space character at the beginning or end of the value.</span></span> <span data-ttu-id="5f989-210">В элементе **ida:ClientKey** укажите *ключ*, сохраненный из каталога.</span><span class="sxs-lookup"><span data-stu-id="5f989-210">For the **ida:ClientKey** key, use the *key*  that you saved from the directory.</span></span> <span data-ttu-id="5f989-211">Опять-таки, не добавляйте пробелы и не меняйте значение каким-либо другим образом.</span><span class="sxs-lookup"><span data-stu-id="5f989-211">Again, be careful not to introduce any space characters or change the value in any way.</span></span> <span data-ttu-id="5f989-212">Теперь раздел `<appSettings>` должен выглядеть примерно так (значением **ClientId** может быть GUID или пустая строка):</span><span class="sxs-lookup"><span data-stu-id="5f989-212">The `<appSettings>` section should now look something like the following (the **ClientId** value may have a GUID or an empty string):</span></span>
    
  ```
    <appSettings>
      <add key="ClientId" value="" />
      <add key="ClientSecret" value="LypZu2yVajlHfPLRn5J2hBrwCk5aBOHxE4PtKCjIQkk=" />
      <add key="ida:ClientID" value="4da99afe-08b5-4bce-bc66-5356482ec2df" />
      <add key="ida:ClientKey" value="URwh/oiPay/b5jJWYHgkVdoE/x7gq3zZdtcl/cG14ss=" />
    </appSettings>
  ```

  > [!NOTE] 
  > Azure AD идентифицирует приложение по URL-адресу localhost, который использовался для его регистрации. Идентификатор и ключ клиента сопоставлены с этим удостоверением. <span data-ttu-id="5f989-215">Когда вы будете готовы разместить приложение на веб-сайте Azure, вы повторно зарегистрируете его с новым URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="5f989-215">Note Your application is known to Azure AD by the "localhost" URL you used to register it. The client ID and client key are associated with that identity. When you are ready to stage your application to an Azure Web Site, you will re-register it with a new URL.</span></span>

4. <span data-ttu-id="5f989-216">Не покидая раздел **appSettings**, добавьте ключ **Authority** и укажите в качестве его значения домена Office 365 (*домен*.onmicrosoft.com) своей организационной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5f989-216">Still in the  **appSettings** section, add an **Authority** key and set its value to the Office 365 domain ( *some_domain*  .onmicrosoft.com) of your organizational account. In the continuing example, the organizational account is Bob@<O365_domain>.onmicrosoft.com, so the authority is .</span></span> <span data-ttu-id="5f989-217">В нашем примере используется организационная учетная запись `Bob@<O365_domain>.onmicrosoft.com`, поэтому указывается домен `<O365_domain>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="5f989-217">In the continuing example, the organizational account is `Bob@<O365_domain>.onmicrosoft.com`, so the authority is `<O365_domain>.onmicrosoft.com`.</span></span> 
    
  ```
    <add key="Authority" value="<O365_domain>.onmicrosoft.com" />
  ```

5. <span data-ttu-id="5f989-218">В разделе **appSettings** добавьте ключ **AppRedirectUrl** и укажите в качестве его значения страницу, на которую должен перенаправляться браузер пользователя, когда надстройка ASP.NET получит код авторизации от Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f989-218">Still in the  **appSettings** section, add an **AppRedirectUrl** key and set its value to the page that the user's browser should be redirected to after the ASP.NET add-in has obtained an authorization code from Azure AD. Usually, this is the same page that the user was on when the call to Azure AD was made. In the continuing example, use the SSL URL value with "/Pages/Default.aspx" appended to it as shown below. (This is another value that you will change for staging.)</span></span> <span data-ttu-id="5f989-219">Как правило, это та же страница, которую просматривал пользователь на момент вызова Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f989-219">Usually, this is the same page that the user was on when the call to Azure AD was made.</span></span> <span data-ttu-id="5f989-220">В нашем примере используется значение URL-адреса SSL, к которому добавлена строка "/Pages/Default.aspx", как показано в следующем фрагменте кода (это еще одно значение, которое потребуется изменить для размещения):</span><span class="sxs-lookup"><span data-stu-id="5f989-220">In the continuing example, use the SSL URL value with "/Pages/Default.aspx" appended to it as shown in the following code (this is another value that you will change for staging):</span></span>
    
  ```
    <add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />
  ```

6. <span data-ttu-id="5f989-221">Не покидая раздел **appSettings**, добавьте ключ **ResourceUrl** и задайте в качестве его значения URI идентификатора приложения шлюза SAP для Майкрософт, а *не* URI идентификатора приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5f989-221">Still in the  **appSettings** section, add a **ResourceUrl** key and set its value to the APP ID URI of SAP Gateway for Microsoft ( *not*  the APP ID URI of your ASP.NET application). Obtain this value from the SAP Gateway for Microsoft administrator. The following is an example.</span></span> <span data-ttu-id="5f989-222">Это значение можно узнать у администратора шлюза SAP для Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5f989-222">Obtain this value from the SAP Gateway for Microsoft administrator.</span></span> <span data-ttu-id="5f989-223">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="5f989-223">The following is an example.</span></span>
      
  ```
    <add key="ResourceUrl" value="http://<SAP_gateway_domain>.cloudapp.net/" />
  ```

  <span data-ttu-id="5f989-224">Теперь раздел `<appSettings>` должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="5f989-224">The  `<appSettings>` section should now look something like this:</span></span>
    
  ```
    <appSettings>
      <add key="ClientId" value="06af1059-8916-4851-a271-2705e8cf53c6" />
      <add key="ClientSecret" value="LypZu2yVajlHfPLRn5J2hBrwCk5aBOHxE4PtKCjIQkk=" />
      <add key="ida:ClientID" value="4da99afe-08b5-4bce-bc66-5356482ec2df" />
      <add key="ida:ClientKey" value="URwh/oiPay/b5jJWYHgkVdoE/x7gq3zZdtcl/cG14ss=" />
      <add key="Authority" value="<O365_domain>.onmicrosoft.com" />
      <add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />
      <add key="ResourceUrl" value="http://<SAP_gateway_domain>.cloudapp.net/" />
    </appSettings>
  ```

7. <span data-ttu-id="5f989-225">Сохраните и закройте файл web.config.</span><span class="sxs-lookup"><span data-stu-id="5f989-225">Save and close the web.config file.</span></span>
    
  > [!TIP] 
  > <span data-ttu-id="5f989-226">Запуская отладчик Visual Studio (F5), не оставляйте файл web.config открытым.</span><span class="sxs-lookup"><span data-stu-id="5f989-226">Do not leave the web.config file open when you run the Visual Studio debugger (F5).</span></span> <span data-ttu-id="5f989-227">Инструменты разработчика Office для Visual Studio меняют значение **ClientId** (а не **ida:ClientID**) при каждом нажатии клавиши F5.</span><span class="sxs-lookup"><span data-stu-id="5f989-227">The Office Developer Tools for Visual Studio change the **ClientId** value (not the **ida:ClientID**) every time you select F5.</span></span> <span data-ttu-id="5f989-228">При этом вам нужно отреагировать на предложение заново загрузить файл web.config (если он открыт) перед отладкой.</span><span class="sxs-lookup"><span data-stu-id="5f989-228">Do not leave the web.config file open when you run the vsnv debugger (F5). The vstoshort change the ClientId value (not the ida:ClientID) every time you press F5. This requires you to respond to a prompt to reload the web.config file, if it is open, before debugging can execute.</span></span>


### <a name="to-add-a-helper-class-to-authenticate-to-azure-ad"></a><span data-ttu-id="5f989-229">Добавление вспомогательного класса для проверки подлинности в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f989-229">Add a helper class to authenticate to Azure AD</span></span>

1. <span data-ttu-id="5f989-230">Щелкните проект ASP.NET правой кнопкой мыши и следуйте процессу добавления элемента Visual Studio, чтобы добавить к проекту новый файл класса с именем **AADAuthHelper.cs**.</span><span class="sxs-lookup"><span data-stu-id="5f989-230">Right-click the ASP.NET project and use the Visual Studio item adding process to add a new class file to the project named AADAuthHelper.cs.</span></span>

2. <span data-ttu-id="5f989-231">Добавьте в файл приведенные ниже операторы **using**.</span><span class="sxs-lookup"><span data-stu-id="5f989-231">Add the following **using** statements to the file.</span></span>
    
  ```
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Configuration;
    using System.Web.UI;
  ```

3. <span data-ttu-id="5f989-232">Измените ключевое слово доступа с **public** на **internal** и добавьте ключевое слово **static** к объявлению класса.</span><span class="sxs-lookup"><span data-stu-id="5f989-232">Change the access keyword from **public** to **internal** and add the **static** keyword to the class declaration.</span></span>
    
  ```
    internal static class AADAuthHelper
  ```

4. <span data-ttu-id="5f989-233">Добавьте в класс приведенные ниже поля.</span><span class="sxs-lookup"><span data-stu-id="5f989-233">Add the following fields to the  Default class.</span></span> <span data-ttu-id="5f989-234">В этих полях хранятся сведения, с помощью которых приложение ASP.NET получает маркеры доступа из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f989-234">Add the following fields to the class. These fields store information that your ASP.NET application uses to get access tokens from AAD.</span></span>
    
  ```
    private static readonly string _authority = ConfigurationManager.AppSettings["Authority"];
    private static readonly string _appRedirectUrl = ConfigurationManager.AppSettings["AppRedirectUrl"];
    private static readonly string _resourceUrl = ConfigurationManager.AppSettings["ResourceUrl"];     
    private static readonly string _clientId = ConfigurationManager.AppSettings["ida:ClientID"];        
    private static readonly ClientCredential _clientCredential = new ClientCredential(
                              ConfigurationManager.AppSettings["ida:ClientID"],
                              ConfigurationManager.AppSettings["ida:ClientKey"]);

    private static readonly AuthenticationContext _authenticationContext = 
                new AuthenticationContext("https://login.windows.net/common/" + 
                                          ConfigurationManager.AppSettings["Authority"]);
  ```

5. <span data-ttu-id="5f989-235">Добавьте в класс приведенное ниже свойство.</span><span class="sxs-lookup"><span data-stu-id="5f989-235">Add the following properties to the class.</span></span> <span data-ttu-id="5f989-236">Это свойство содержит URL-адрес экрана входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f989-236">Add the following property to the class. This property holds the URL to the Azure AD login screen.</span></span>
    
  ```
      private static string AuthorizeUrl
    {
        get
        {
            return string.Format("https://login.windows.net/{0}/oauth2/authorize?response_type=code&amp;redirect_uri={1}&amp;client_id={2}&amp;state={3}",
                _authority,
                _appRedirectUrl,
                _clientId,
                Guid.NewGuid().ToString());
        }
    }
  ```

6. <span data-ttu-id="5f989-p137">Добавьте в класс приведенные ниже свойства. Они кэшируют маркеры доступа и обновления, а также проверяют, действительны ли они.</span><span class="sxs-lookup"><span data-stu-id="5f989-p137">Add the following properties to the class. These cache the access and refresh tokens and check their validity.</span></span>
    
  ```
      public static Tuple<string, DateTimeOffset> AccessToken
    {
        get { return HttpContext.Current.Session["AccessTokenWithExpireTime-" + _resourceUrl] 
          as Tuple<string, DateTimeOffset>;
        }

        set { HttpContext.Current.Session["AccessTokenWithExpireTime-" + _resourceUrl] = value; }
    }

    private static bool IsAccessTokenValid
    {
      get { 
          return AccessToken != null &amp;&amp;
          !string.IsNullOrEmpty(AccessToken.Item1) &amp;&amp;
          AccessToken.Item2 > DateTimeOffset.UtcNow;
      }
    }

    private static string RefreshToken
    {
        get { return HttpContext.Current.Session["RefreshToken" + _resourceUrl] as string; }
        set { HttpContext.Current.Session["RefreshToken-" + _resourceUrl] = value; }
    }

    private static bool IsRefreshTokenValid
    {
        get { return !string.IsNullOrEmpty(RefreshToken); }
    }

  ```

7. <span data-ttu-id="5f989-p138">Добавьте к классу следующие методы. Они используются для проверки кода аутентификации и получения маркера доступа из Azure AD с помощью кода авторизации или маркера обновления.</span><span class="sxs-lookup"><span data-stu-id="5f989-p138">Add the following methods to the class. These are used to check the validity of the authorization code and to obtain an access token from Azure AD by using either an authentication code or a refresh token.</span></span>
    
  ```
    private static bool IsAuthorizationCodeNotNull(string authCode)
    {
        return !string.IsNullOrEmpty(authCode);
    }

    private static Tuple<Tuple<string,DateTimeOffset>,string> AcquireTokensUsingAuthCode(string authCode)
    {
        var authResult = _authenticationContext.AcquireTokenByAuthorizationCode(
                    authCode,
                    new Uri(_appRedirectUrl),
                    _clientCredential,
                    _resourceUrl);

        return new Tuple<Tuple<string, DateTimeOffset>, string>(
                    new Tuple<string, DateTimeOffset>(authResult.AccessToken, authResult.ExpiresOn), 
                    authResult.RefreshToken);
    }

    private static Tuple<string, DateTimeOffset> RenewAccessTokenUsingRefreshToken()
    {
        var authResult = _authenticationContext.AcquireTokenByRefreshToken(
                            RefreshToken,
                            _clientCredential.OwnerId,
                            _clientCredential,
                            _resourceUrl);

        return new Tuple<string, DateTimeOffset>(authResult.AccessToken, authResult.ExpiresOn);
    }

  ```

8. <span data-ttu-id="5f989-241">Добавьте в класс приведенный ниже метод.</span><span class="sxs-lookup"><span data-stu-id="5f989-241">Add the following method to the  class.</span></span> <span data-ttu-id="5f989-242">Он вызывается из кода ASP.NET для получения маркера доступа перед отправкой запроса данных SAP через шлюз SAP для Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5f989-242">Add the following method to the class. It is called from the ASP.NET code behind to obtain a valid access token before a call is made to get SAP data via SAP Gateway for Microsoft.</span></span>
    
  ```
      internal static void EnsureValidAccessToken(Page page)
    {
        if (IsAccessTokenValid) 
        {
            return;
        }
        else if (IsRefreshTokenValid) 
        {
            AccessToken = RenewAccessTokenUsingRefreshToken();
            return;
        }
        else if (IsAuthorizationCodeNotNull(page.Request.QueryString["code"]))
        {
            Tuple<Tuple<string, DateTimeOffset>, string> tokens = null;
            try
            {
                tokens = AcquireTokensUsingAuthCode(page.Request.QueryString["code"]);
            }
            catch 
            {
                page.Response.Redirect(AuthorizeUrl);
            }
            AccessToken = tokens.Item1;
            RefreshToken = tokens.Item2;
            return;
        }
        else
        {
            page.Response.Redirect(AuthorizeUrl);
        }
    }
  ```


> [!TIP] 
> <span data-ttu-id="5f989-243">В классе AADAuthHelper реализован минимум действий по обработке ошибок.</span><span class="sxs-lookup"><span data-stu-id="5f989-243">The AADAuthHelper class has only minimal error handling.</span></span> <span data-ttu-id="5f989-244">Чтобы создать надежную надстройку SharePoint для использования в рабочей среде, добавьте обработку ошибок, как описано в статье [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](https://docs.microsoft.com/ru-RU/azure/active-directory/develop/active-directory-protocols-oauth-code) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="5f989-244">For a robust, production quality SharePoint Add-in, add more error handling as described in this MSDN node: [Authorize access to web applications using OAuth 2.0 and Azure Active Directory](https://docs.microsoft.com/ru-RU/azure/active-directory/develop/active-directory-protocols-oauth-code).</span></span>


### <a name="to-create-data-model-classes"></a><span data-ttu-id="5f989-245">Создание классов модели данных</span><span class="sxs-lookup"><span data-stu-id="5f989-245">To create data model classes</span></span>

1. <span data-ttu-id="5f989-246">Создайте один или несколько классов для моделирования данных, которые надстройка получает из SAP.</span><span class="sxs-lookup"><span data-stu-id="5f989-246">Create one or more classes to model the data that your add-in gets from SAP.</span></span> <span data-ttu-id="5f989-247">В нашем примере используется только один класс модели данных.</span><span class="sxs-lookup"><span data-stu-id="5f989-247">In the continuing example, there is just one data model class.</span></span> <span data-ttu-id="5f989-248">Щелкните проект ASP.NET правой кнопкой мыши и следуйте процессу добавления элемента Visual Studio, чтобы добавить к проекту новый файл класса с именем **Automobile.cs**.</span><span class="sxs-lookup"><span data-stu-id="5f989-248">Right-click the ASP.NET project and use the Visual Studio item adding process to add a new class file to the project named AADAuthHelper.cs.</span></span>

2. <span data-ttu-id="5f989-249">Добавьте в текст класса следующий код:</span><span class="sxs-lookup"><span data-stu-id="5f989-249">Add the following code to the body of the class:</span></span>
    
  ```
    public string Price;
    public string Brand;
    public string Model;
    public int Year;
    public string Engine;
    public int MaxPower;
    public string BodyStyle;
    public string Transmission;
  ```


### <a name="to-add-code-behind-to-get-data-from-sap-via-the-sap-gateway-for-microsoft"></a><span data-ttu-id="5f989-250">Добавление кода для получения данных из SAP через шлюз SAP для Майкрософт</span><span class="sxs-lookup"><span data-stu-id="5f989-250">Add code behind to get data from SAP via the SAP Gateway for Microsoft</span></span>

1. <span data-ttu-id="5f989-251">Откройте файл Default.aspx.cs и добавьте приведенные ниже операторы **using**.</span><span class="sxs-lookup"><span data-stu-id="5f989-251">Open the Default.aspx.cs file and add the following **using** statements.</span></span>
    
  ```
    using System.Net;
    using Newtonsoft.Json.Linq;
  ```

2. <span data-ttu-id="5f989-p142">Добавьте объявление **const** к классу Default, указав в качестве значения URL-адрес конечной точки OData SAP, которую будет использовать надстройку. Вот пример такого объявления:</span><span class="sxs-lookup"><span data-stu-id="5f989-p142">Add a **const** declaration to the Default class whose value is the base URL of the SAP OData endpoint that the add-in will be accessing. The following is an example:</span></span>
    
  ```
      private const string SAP_ODATA_URL = @"https://<SAP_gateway_domain>.cloudapp.net:8081/perf/sap/opu/odata/sap/ZCAR_POC_SRV/";
  ```

3. <span data-ttu-id="5f989-254">В Инструментах разработчика Office для Visual Studio появились методы **Page\_PreInit** и **Page\_Load**.</span><span class="sxs-lookup"><span data-stu-id="5f989-254">The Office Developer Tools for Visual Studio have added a **Page\_PreInit** method and a **Page\_Load** method.</span></span> <span data-ttu-id="5f989-255">Раскомментируйте код метода **Page\_Load** и весь метод **Page\_Init**.</span><span class="sxs-lookup"><span data-stu-id="5f989-255">Comment out the code inside the **Page\_Load** method and comment out the whole **Page\_Init** method.</span></span> <span data-ttu-id="5f989-256">Этот код не используется в нашем примере.</span><span class="sxs-lookup"><span data-stu-id="5f989-256">This code is not used in this sample.</span></span> <span data-ttu-id="5f989-257">Если ваша надстройка SharePoint будет получать доступ к SharePoint, восстановите этот код.</span><span class="sxs-lookup"><span data-stu-id="5f989-257">(If your SharePoint Add-in is going to access SharePoint, restore this code.</span></span> <span data-ttu-id="5f989-258">См. раздел [Предоставление приложению ASP.NET доступа к SharePoint (необязательно)](#SharePoint).</span><span class="sxs-lookup"><span data-stu-id="5f989-258">See [Add SharePoint access to the ASP.NET application (optional)](#SharePoint).)</span></span>

4. <span data-ttu-id="5f989-259">Добавьте приведенную ниже строку в начале метода **Page_Load**.</span><span class="sxs-lookup"><span data-stu-id="5f989-259">Add the following line to the top of the **Page_Load** method.</span></span> <span data-ttu-id="5f989-260">Это упрощает отладку, так как приложение ASP.NET связывается со шлюзом SAP для Майкрософт с помощью протокола SSL (HTTPS), но сервер "localhost:порт" все еще не настроен на доверие сертификату шлюза SAP для Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5f989-260">This eases the process of debugging because your ASP.NET application is communicating with SAP Gateway for Microsoft using SSL (HTTPS), but your "localhost:port" server is not configured to trust the certificate of SAP Gateway for Microsoft.</span></span> <span data-ttu-id="5f989-261">Без этой строки кода перед открытием файла Default.aspx появлялось бы предупреждение о недействительном сертификате.</span><span class="sxs-lookup"><span data-stu-id="5f989-261">Without this line of code, you would get an invalid certificate warning before Default.aspx opens.</span></span> <span data-ttu-id="5f989-262">В одних браузерах можно пропустить эту ошибку, а в других открыть файл Default.aspx будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="5f989-262">Some browsers allow you to click past this error, but some will not let you open Default.aspx at all.</span></span>
    
  ```
    ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;
  ```

  > [!IMPORTANT] 
  > <span data-ttu-id="5f989-263">Удалите эту строку, когда вы будете готовы к развертыванию приложения ASP.NET для его размещения.</span><span class="sxs-lookup"><span data-stu-id="5f989-263">Delete this line when you are ready to deploy the ASP.NET application to staging. See Modify the app and stage it to Azure and Office 365.</span></span> <span data-ttu-id="5f989-264">См. раздел [Изменение и размещение надстройки в Azure и Office 365](#Stage).</span><span class="sxs-lookup"><span data-stu-id="5f989-264">Modify the add-in and stage it to Azure and Office 365</span></span>

5. <span data-ttu-id="5f989-p146">Добавьте приведенный ниже код в метод **Page_Load**. Строка, передаваемая методу `GetSAPData`, — это запрос OData.</span><span class="sxs-lookup"><span data-stu-id="5f989-p146">Add the following code to the **Page_Load** method. The string you pass to the `GetSAPData` method is an OData query.</span></span>
    
  ```
    if (!IsPostBack)
  {
      GetSAPData("DataCollection?$top=3");
  }
  ```

6. <span data-ttu-id="5f989-p147">Добавьте следующий метод к классу Default. Этот метод сначала обеспечивает наличие в кэше действительного маркера доступа, полученного из Azure AD, а затем создает HTTP-запрос **GET**, который включает маркер доступа и отправляет его конечной точке OData SAP. Возвращаемый результат является объектом JSON, преобразованным в объект .NET **List**. В массиве, связанном с **DataListView**, используются три свойства элементов.</span><span class="sxs-lookup"><span data-stu-id="5f989-p147">Add the following method to the Default class. This method first ensures that the cache for the access token has a valid access token in it that has been obtained from Azure AD. It then creates an HTTP **GET** Request that includes the access token and sends it to the SAP OData endpoint. The result is returned as a JSON object that is converted to a .NET **List** object. Three properties of the items are used in an array that is bound to the **DataListView**.</span></span>
    
  ```
      private void GetSAPData(string oDataQuery)
    {
        AADAuthHelper.EnsureValidAccessToken(this);

        using (WebClient client = new WebClient())
        {
            client.Headers[HttpRequestHeader.Accept] = "application/json";
            client.Headers[HttpRequestHeader.Authorization] = "Bearer " + AADAuthHelper.AccessToken.Item1;
            var jsonString = client.DownloadString(SAP_ODATA_URL + oDataQuery);
            var jsonValue = JObject.Parse(jsonString)["d"]["results"];
            var dataCol = jsonValue.ToObject<List<Automobile>>();

            var dataList = dataCol.Select((item) => {
                return item.Brand + " " + item.Model + " " + item.Price;
                }).ToArray();

            DataListView.DataSource = dataList;
            DataListView.DataBind();
        }
    }

  ```


### <a name="to-create-the-user-interface"></a><span data-ttu-id="5f989-272">Создание пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="5f989-272">To create the user interface</span></span>


1. <span data-ttu-id="5f989-273">Откройте файл Default.aspx и добавьте следующую разметку к объекту **form**:</span><span class="sxs-lookup"><span data-stu-id="5f989-273">Open the Default.aspx file and add the following markup to the **form** of the page:</span></span>
    
    ```
      <div>
      <h3>Data from SAP via SAP Gateway for Microsoft</h3>

      <asp:ListView runat="server" ID="DataListView">
        <ItemTemplate>
          <tr runat="server">
            <td runat="server">
              <asp:Label ID="DataLabel" runat="server"
                Text="<%# Container.DataItem.ToString()%>" /><br />
            </td>
          </tr>
        </ItemTemplate>
      </asp:ListView>
    </div>
    ```

2. <span data-ttu-id="5f989-274">При желании вы можете придать веб-странице внешний вид страницы SharePoint с помощью [элемента управления хрома](use-the-client-chrome-control-in-sharepoint-add-ins.md) SharePoint и [таблицы стилей веб-сайта SharePoint](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="5f989-274">Optionally, give the web page the "look 'n' feel" of a SharePoint page with the SharePoint  [Chrome Control](use-the-client-chrome-control-in-sharepoint-add-ins.md) and [the host SharePoint website's style sheet](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md).</span></span>
    
 
### <a name="to-test-the-add-in-with-f5-in-visual-studio"></a><span data-ttu-id="5f989-275">Тестирование надстройки с помощью клавиши F5 в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5f989-275">Test the add-in with F5 in Visual Studio</span></span>

1. <span data-ttu-id="5f989-276">Нажмите клавишу F5 в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f989-276">Press F5 in Visual Studio.</span></span>   
 
2. <span data-ttu-id="5f989-277">После первого нажатия клавиши F5 вам может быть предложено войти на используемый сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="5f989-277">The first time that you use F5, you may be prompted to login to the Developer Site that you are using. Use the site administrator credentials. In the continuing example, it is Bob@<O365_domain>.onmicrosoft.com.</span></span> <span data-ttu-id="5f989-278">Используйте учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="5f989-278">Use the site administrator credentials.</span></span> <span data-ttu-id="5f989-279">В нашем примере это учетная запись `Bob@<O365_domain>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="5f989-279">Open the application you created. In the continuing example, it is  `Bob@<O365_domain>.onmicrosoft.com`.</span></span>    
 
3. <span data-ttu-id="5f989-280">При первом нажатии клавиши F5 вам будет предложено предоставить надстройке разрешения.</span><span class="sxs-lookup"><span data-stu-id="5f989-280">The first time that you use F5, you are prompted to grant permissions to the add-in. Click  Trust It.</span></span> <span data-ttu-id="5f989-281">Нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="5f989-281">Select the **Trust It** button.</span></span>    
 
4. <span data-ttu-id="5f989-p150">После краткой задержки для получения маркера доступа открывается страница Default.aspx. Убедитесь, что на ней отображаются данные SAP.</span><span class="sxs-lookup"><span data-stu-id="5f989-p150">After a brief delay while the access token is being obtained, the Default.aspx page opens. Verify that the SAP data appears.</span></span>
    

<span data-ttu-id="5f989-284"><a name="SharePoint"> </a></span><span class="sxs-lookup"><span data-stu-id="5f989-284"></span></span> 

## <a name="add-sharepoint-access-to-the-aspnet-application-optional"></a><span data-ttu-id="5f989-285">Предоставление приложению ASP.NET доступа к SharePoint (необязательно)</span><span class="sxs-lookup"><span data-stu-id="5f989-285">Optionally, add SharePoint access to the ASP.NET application</span></span>

<span data-ttu-id="5f989-286">Конечно, надстройка SharePoint может не только выводить данные SAP на веб-странице, открытой из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f989-286">Of course, your SharePoint Add-in doesn't have to expose only SAP data in a web page launched from SharePoint.</span></span> <span data-ttu-id="5f989-287">Она также может выполнять операции CRUD (создание, чтение, обновление и удаление) с данными из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f989-287">It can also create, read, update, and delete (CRUD) SharePoint data.</span></span> <span data-ttu-id="5f989-288">Для этого в коде можно использовать либо клиентскую объектную модель SharePoint (CSOM), либо интерфейсы REST API для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f989-288">Your code-behind can do this by using either the SharePoint client object model (CSOM) or the REST APIs of SharePoint.</span></span> <span data-ttu-id="5f989-289">CSOM развертывается в виде пары сборок, которые Инструменты разработчика Office для Visual Studio автоматически включают в проект ASP.NET, задавая параметр **Копировать локально** в Visual Studio, чтобы они добавлялись в пакет приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5f989-289">The CSOM is deployed as a pair of assemblies that the Office Developer Tools for Visual Studio automatically included in the ASP.NET project and set to **Copy Local** in Visual Studio so that they are included in the ASP.NET application package.</span></span> 

<span data-ttu-id="5f989-290">Общие сведения о CSOM см. в статье [Выполнение базовых операций с использованием кода клиентской библиотеки SharePoint](complete-basic-operations-using-sharepoint-client-library-code.md).</span><span class="sxs-lookup"><span data-stu-id="5f989-290">For information about using CSOM, start with [Complete basic operations using SharePoint client library code](complete-basic-operations-using-sharepoint-client-library-code.md).</span></span> <span data-ttu-id="5f989-291">Общие сведения об использовании интерфейсов REST API см. в статье [Знакомство с REST-интерфейсом SharePoint 2013 и его использование](https://msdn.microsoft.com/ru-RU/magazine/dn198245.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f989-291">For information about using the REST APIs, start with  [Understanding and Using the SharePoint REST Interface](https://msdn.microsoft.com/ru-RU/magazine/dn198245.aspx).</span></span> 

<span data-ttu-id="5f989-292">Независимо от того, используется ли CSOM или REST API для доступа к SharePoint, приложение ASP.NET должно получить маркер доступа к SharePoint, как и в случае шлюза SAP для Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5f989-292">Regardless, of whether you use CSOM or the REST APIs to access SharePoint, your ASP.NET application must get an access token to SharePoint, just as it does to SAP Gateway for Microsoft. See  Understand authentication and authorization to SAP Gateway for Microsoft and SharePoint above. The procedure below provides some basic guidance about how to do this, but we recommend that you first read the following articles:</span></span> <span data-ttu-id="5f989-293">См. раздел [Общие сведения о проверке подлинности и авторизации в шлюзе SAP для Майкрософт и SharePoint](#AuthOverview) ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5f989-293">Understand authentication and authorization to SAP Gateway for Microsoft and SharePoint</span></span> 

<span data-ttu-id="5f989-294">Ниже представлены основные инструкции по выполнению этой задачи, но для начала рекомендуем ознакомиться со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="5f989-294">The following procedure provides some basic guidance about how to do this, but we recommend that you first read these articles:</span></span>

-  [<span data-ttu-id="5f989-295">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="5f989-295">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
-  [<span data-ttu-id="5f989-296">Авторизация и проверка подлинности для надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f989-296">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins.md)
-  [<span data-ttu-id="5f989-297">Три системы авторизации для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f989-297">Three authorization systems for SharePoint Add-ins</span></span>](three-authorization-systems-for-sharepoint-add-ins.md)   
-  [<span data-ttu-id="5f989-298">Создание надстроек SharePoint, использующих авторизацию с низким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="5f989-298">Creating SharePoint Add-ins that use low-trust authorization</span></span>](creating-sharepoint-add-ins-that-use-low-trust-authorization.md)    
-  [<span data-ttu-id="5f989-299">Поток OAuth токена контекста для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f989-299">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins.md)   
 
### <a name="to-add-sharepoint-access-to-the-aspnet-application"></a><span data-ttu-id="5f989-300">Предоставление приложению ASP.NET доступа к SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f989-300">Optionally, add SharePoint access to the ASP.NET application</span></span>

1. <span data-ttu-id="5f989-301">Откройте файл Default.aspx.cs и раскомментируйте метод **Page\_PreInit**.</span><span class="sxs-lookup"><span data-stu-id="5f989-301">Open the Default.aspx.cs file and uncomment the **Page\_PreInit** method.</span></span> <span data-ttu-id="5f989-302">Кроме того, раскомментируйте код, который Инструменты разработчика Office для Visual Studio добавили к методу **Page\_Load**.</span><span class="sxs-lookup"><span data-stu-id="5f989-302">Open the Default.aspx.cs file and uncomment the  Page_PreInit method. Also uncomment the code that the Office Developer Tools for Visual Studio added to the **Page_Load** method.</span></span>

2. <span data-ttu-id="5f989-303">Если надстройка SharePoint будет получать доступ к данным SharePoint, необходимо кэшировать токен контекста SharePoint, отправляемый странице Default.aspx с помощью запроса POST при запуске надстройки в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f989-303">If your SharePoint Add-in is going to access SharePoint data, you have to cache the SharePoint context token that is POSTed to the Default.aspx page when the add-in is launched in SharePoint.</span></span> <span data-ttu-id="5f989-304">Это гарантирует, что токен контекста SharePoint не будет потерян при перенаправлении браузера после проверки подлинности в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f989-304">This is to ensure that the SharePoint context token is not lost when the browser is redirected following the Azure AD authentication.</span></span> <span data-ttu-id="5f989-305">Кэшировать этот контекст можно несколькими способами. Инструменты разработчика Office для Visual Studio добавляют к проекту ASP.NET файл SharePointContext.cs, выполняющий большую часть работы.</span><span class="sxs-lookup"><span data-stu-id="5f989-305">(You have several options for how to cache this context.) The Office Developer Tools for Visual Studio add a SharePointContext.cs file to the ASP.NET project that does most of the work.</span></span> <span data-ttu-id="5f989-306">Чтобы использовать кэш сеанса, просто добавьте приведенный ниже код в блок `if (!IsPostBack)` *перед* кодом, который вызывает шлюз SAP для Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5f989-306">To use the session cache, you simply add the following code inside the `if (!IsPostBack)` block *before* the code that calls out to SAP Gateway for Microsoft.</span></span>
      
  ```
      if (HttpContext.Current.Session["SharePointContext"] == null) 
    {
        HttpContext.Current.Session["SharePointContext"]
            = SharePointContextProvider.Current.GetSharePointContext(Context);
    }
  ```

3. <span data-ttu-id="5f989-p156">Файл SharePointContext.cs отправляет вызовы другому файлу, который Инструменты разработчика Office для Visual Studio добавляет к проекту: TokenHelper.cs. Этот файл содержит большую часть кода, необходимого для получения и использования маркеров доступа для SharePoint. Тем не менее, в нем отсутствует код для продления срока действия устаревшего маркера доступа или маркера обновления. Кроме того, в нем нет кода для кэширования маркеров. Если вы создаете профессиональную надстройку SharePoint, добавить этот код необходимо. Примером может служить логика кэширования из предыдущего этапа. Ваш код также должен кэшировать маркер доступа и продолжать использовать его до истечения срока действия. По истечении срока действия маркера код должен получить новый маркер доступа с помощью маркера обновления.</span><span class="sxs-lookup"><span data-stu-id="5f989-p156">The SharePointContext.cs file makes calls to another file that the Office Developer Tools for Visual Studio added to the project: TokenHelper.cs. This file provides most of the code needed to obtain and use access tokens for SharePoint. However, it does not provide any code for renewing an expired access token or an expired refresh token. Nor does it contain any token caching code. For a production quality SharePoint Add-in, you need to add such code. The caching logic in the preceding step is an example. Your code should also cache the access token and reuse it until it expires. When the access token is expired, your code should use the refresh token to get a new access token.</span></span>
 
4. <span data-ttu-id="5f989-315">Добавьте вызовы данных из SharePoint с помощью CSOM или REST.</span><span class="sxs-lookup"><span data-stu-id="5f989-315">Add the data calls to SharePoint by using either CSOM or REST.</span></span> <span data-ttu-id="5f989-316">Приведенный ниже пример представляет собой измененный код CSOM, который Инструменты разработчика Office для Visual Studio добавляют к методу **Page_Load**.</span><span class="sxs-lookup"><span data-stu-id="5f989-316">The following example is a modification of CSOM code that Office Developer Tools for Visual Studio adds to the **Page_Load** method.</span></span> <span data-ttu-id="5f989-317">В этом примере код был перемещен в отдельный метод и начинается с получения кэшированного токена контекста.</span><span class="sxs-lookup"><span data-stu-id="5f989-317">Add the data calls to spnv using either CSOM or REST. The following example is a modification of CSOM code that vstoshort adds to the Page_Load method. In this example, the code has been moved to a separate method and it begins by retrieving the cached context token.</span></span>
    
  ```
      private void GetSharePointTitle()
    {
        var spContext = HttpContext.Current.Session["SharePointContext"] as SharePointContext;
        using (var clientContext = spContext.CreateUserClientContextForSPHost())
        {
            clientContext.Load(clientContext.Web, web => web.Title);
            clientContext.ExecuteQuery();
            SharePointTitle.Text = "SharePoint web site title is: " + clientContext.Web.Title;
        }
    }
  ```

5. <span data-ttu-id="5f989-p158">Добавьте элементы пользовательского интерфейса для отрисовки данных SharePoint. Ниже показан элемент управления HTML, на который ссылается предыдущий метод.</span><span class="sxs-lookup"><span data-stu-id="5f989-p158">Add UI elements to render the SharePoint data. The following shows the HTML control that is referenced in the preceding method:</span></span>
    
  ```HTML
    <h3>SharePoint title</h3><asp:Label ID="SharePointTitle" runat="server"></asp:Label><br />
  ```

  > [!NOTE] 
  > <span data-ttu-id="5f989-320">Во время отладки надстройки SharePoint Инструменты разработчика Office для Visual Studio заново регистрируют ее в Azure ACS при каждом нажатии клавиши F5 в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f989-320">Note  While you are debugging the SharePoint Add-in, the Office Developer Tools for Visual Studio re-register it with Azure ACS each time you press F5 in Visual Studio. When you stage the SharePoint Add-in, you have to give it a long-term registration. See the section  Modify the add-in and stage it to Azure and Office 365.</span></span> <span data-ttu-id="5f989-321">При размещении надстройки SharePoint необходимо выполнить долгосрочную регистрацию.</span><span class="sxs-lookup"><span data-stu-id="5f989-321">When you stage the SharePoint Add-in, you have to give it a long-term registration.</span></span> <span data-ttu-id="5f989-322">См. раздел [Изменение и размещение надстройки в Azure и Office 365](#Stage).</span><span class="sxs-lookup"><span data-stu-id="5f989-322">Modify the add-in and stage it to Azure and Office 365</span></span>
 

<span data-ttu-id="5f989-323"><a name="Stage"> </a></span><span class="sxs-lookup"><span data-stu-id="5f989-323"></span></span>

## <a name="modify-the-add-in-and-stage-it-to-azure-and-office-365"></a><span data-ttu-id="5f989-324">Изменение и размещение надстройки в Azure и Office 365</span><span class="sxs-lookup"><span data-stu-id="5f989-324">Modify the add-in and stage it to Azure and Office 365</span></span>

<span data-ttu-id="5f989-325">Закончив отлаживать надстройку SharePoint с помощью клавиши F5 в Visual Studio, необходимо выполнить развертывание приложения ASP.NET в Веб-сайт Azure.</span><span class="sxs-lookup"><span data-stu-id="5f989-325">When you have finished debugging the SharePoint Add-in using F5 in Visual Studio, you need to deploy the ASP.NET application to an actual Azure Web Site.</span></span>

### <a name="to-create-the-azure-web-site"></a><span data-ttu-id="5f989-326">Создание веб-сайта Azure</span><span class="sxs-lookup"><span data-stu-id="5f989-326">To create the Azure Web Site</span></span>

1. <span data-ttu-id="5f989-327">На портале Microsoft Azure выберите **ВЕБ-САЙТЫ** в левой области навигации.</span><span class="sxs-lookup"><span data-stu-id="5f989-327">In the Microsoft Azure portal, open **WEB SITES** on the left navigation bar.</span></span>
    
2. <span data-ttu-id="5f989-328">Нажмите **СОЗДАТЬ** в нижней части страницы, а в диалоговом окне **СОЗДАНИЕ** выберите команды **ВЕБ-САЙТ** |**БЫСТРОЕ СОЗДАНИЕ**.</span><span class="sxs-lookup"><span data-stu-id="5f989-328">Click **NEW** at the bottom of the page and on the **NEW** dialog select **WEB SITE** |**QUICK CREATE**.</span></span>
    
3. <span data-ttu-id="5f989-329">Введите доменное имя и нажмите кнопку **СОЗДАТЬ ВЕБ-САЙТ**.</span><span class="sxs-lookup"><span data-stu-id="5f989-329">Enter a domain name and select **CREATE WEB SITE**.</span></span> <span data-ttu-id="5f989-330">Скопируйте URL-адрес нового сайта.</span><span class="sxs-lookup"><span data-stu-id="5f989-330">Make a copy of the new site's URL.</span></span> <span data-ttu-id="5f989-331">Он представлен в формате `my_domain.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5f989-331">It has the form  `my_domain.azurewebsites.net`.</span></span>
    
 

### <a name="to-modify-the-code-and-markup-in-the-application"></a><span data-ttu-id="5f989-332">Изменение кода и разметки в приложении</span><span class="sxs-lookup"><span data-stu-id="5f989-332">Modify the code and markup in the application</span></span>

1. <span data-ttu-id="5f989-333">В Visual Studio удалите строку `ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;` из файла Default.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="5f989-333">In Visual Studio, remove the line  `ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;` from the Default.aspx.cs file.</span></span>    
 
2. <span data-ttu-id="5f989-p161">Откройте файл web.config проекта ASP.NET и замените доменную часть значения ключа **AppRedirectUrl** в разделе **appSettings** на домен Веб-сайт Azure. Например, замените `<add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />` на `<add key="AppRedirectUrl" value="https://my_domain.azurewebsites.net/Pages/Default.aspx" />`.</span><span class="sxs-lookup"><span data-stu-id="5f989-p161">Open the web.config file of the ASP.NET project and change the domain part of the value of the **AppRedirectUrl** key in the **appSettings** section to the domain of the Azure Web Site. For example, change `<add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />` to `<add key="AppRedirectUrl" value="https://my_domain.azurewebsites.net/Pages/Default.aspx" />`.</span></span>    
 
3. <span data-ttu-id="5f989-336">Щелкните правой кнопкой мыши файл AppManifest.xml в проекте надстройки SharePoint и выберите команду **Перейти к коду**.</span><span class="sxs-lookup"><span data-stu-id="5f989-336">Right-click the AppManifest.xml file in the SharePoint Add-in project and select **View Code**.</span></span>    
 
4. <span data-ttu-id="5f989-337">В значении **StartPage** замените строку `~remoteAppUrl` на полный домен веб-сайта Azure, включая протокол. Пример: `https://my_domain.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5f989-337">In the  **StartPage** value, replace the string `~remoteAppUrl` with the full domain of the Azure Web Site including the protocol; for example `https://my_domain.azurewebsites.net`. The entire  StartPage value should now be: . (Usually, the  StartPage value is exactly the same as the value of the AppRedirectUrl key in the web.config file.)</span></span> <span data-ttu-id="5f989-338">Теперь полное значение **StartPage** должно выглядеть так: `https://my_domain.azurewebsites.net/Pages/Default.aspx` (как правило, значение **StartPage** полностью совпадает со значением ключа **AppRedirectUrl** в файле web.config).</span><span class="sxs-lookup"><span data-stu-id="5f989-338">In the  StartPage value, replace the string  with the full domain of the Azure Web Site including the protocol; for example . The entire  **StartPage** value should now be: `https://my_domain.azurewebsites.net/Pages/Default.aspx`. (Usually, the  **StartPage** value is exactly the same as the value of the **AppRedirectUrl** key in the web.config file.)</span></span>
    
 

### <a name="to-modify-the-azure-ad-registration-and-register-the-add-in-with-acs"></a><span data-ttu-id="5f989-339">Изменение регистрационных данных в Azure AD и регистрация надстройки в службе контроля доступа</span><span class="sxs-lookup"><span data-stu-id="5f989-339">To modify the Azure AD registration and register the add-in with ACS</span></span>

1. <span data-ttu-id="5f989-340">Войдите на [портал управления Azure](https://manage.windowsazure.com), используя учетную запись администратора Azure.</span><span class="sxs-lookup"><span data-stu-id="5f989-340">Login into the  [Azure Management portal](https://manage.windowsazure.com) with your Azure administrator account.</span></span>    
 
2. <span data-ttu-id="5f989-341">Выберите **Active Directory** в левой части страницы.</span><span class="sxs-lookup"><span data-stu-id="5f989-341">Choose  **Active Directory** on the left side.</span></span>    
 
3. <span data-ttu-id="5f989-342">Выберите каталог.</span><span class="sxs-lookup"><span data-stu-id="5f989-342">Select your directory.</span></span>    
 
4. <span data-ttu-id="5f989-343">Выберите **ПРИЛОЖЕНИЯ** (на верхней панели навигации).</span><span class="sxs-lookup"><span data-stu-id="5f989-343">Choose **APPLICATIONS** (on the top navigation bar).</span></span>    
 
5. <span data-ttu-id="5f989-p163">Откройте созданное приложение. В нашем примере используется имя **ContosoAutomobileCollection**.</span><span class="sxs-lookup"><span data-stu-id="5f989-p163">Open the application you created. In the continuing example, it is **ContosoAutomobileCollection**.</span></span>    
 
6. <span data-ttu-id="5f989-346">В каждом из следующих значений замените фрагмент "localhost: *порт*" на значение домена нового веб-сайта Azure:</span><span class="sxs-lookup"><span data-stu-id="5f989-346">For each of the following values, change the "localhost: *port*  " part of the value to the domain of your new Azure Web Site:</span></span>
    
  - <span data-ttu-id="5f989-347">**URL-АДРЕС ДЛЯ ВХОДА**</span><span class="sxs-lookup"><span data-stu-id="5f989-347">**SIGN-ON URL**</span></span>
      
  - <span data-ttu-id="5f989-348">**URI ИДЕНТИФИКАТОРА ПРИЛОЖЕНИЯ**</span><span class="sxs-lookup"><span data-stu-id="5f989-348">**APP ID URI**</span></span>
      
  - <span data-ttu-id="5f989-349">**URL-АДРЕС ОТВЕТА**</span><span class="sxs-lookup"><span data-stu-id="5f989-349">**REPLY URL**</span></span>
    
  <span data-ttu-id="5f989-350">Например, если для **URI ИДЕНТИФИКАТОРА ПРИЛОЖЕНИЯ** задано значение `https://localhost:44304/ContosoAutomobileCollection`, замените его на `https://<my_domain>.azurewebsites.net/ContosoAutomobileCollection`.</span><span class="sxs-lookup"><span data-stu-id="5f989-350">For example, if the  **APP ID URI** is `https://localhost:44304/ContosoAutomobileCollection`, change it to  `https://<my_domain>.azurewebsites.net/ContosoAutomobileCollection`.</span></span>
    
7. <span data-ttu-id="5f989-351">Нажмите кнопку **СОХРАНИТЬ** в нижней части экрана.</span><span class="sxs-lookup"><span data-stu-id="5f989-351">Click  **SAVE** at the bottom of the screen.</span></span>
    
8. <span data-ttu-id="5f989-352">Зарегистрируйте надстройку в Azure ACS.</span><span class="sxs-lookup"><span data-stu-id="5f989-352">Register the add-in with Azure AD v2.0 endpoint</span></span> <span data-ttu-id="5f989-353">Это необходимо сделать, даже если надстройка не получает доступ к SharePoint и не использует токены из ACS, так как в ходе этого процесса надстройка также регистрируется в службе управления надстройками для подписки на Office 365, что является обязательным условием.</span><span class="sxs-lookup"><span data-stu-id="5f989-353">This must be done even if the add-in does not access SharePoint and does not use tokens from ACS because the same process also registers the add-in with the Add-in Management Service of the Office 365 subscription, which is a requirement.</span></span> <span data-ttu-id="5f989-354">(Название "служба управления надстройками" связано с тем, что изначально надстройки SharePoint назывались "приложениями для SharePoint".)</span><span class="sxs-lookup"><span data-stu-id="5f989-354">(It is called "Add-in Management Service" because SharePoint Add-ins were originally called "apps for SharePoint".)</span></span> 

  <span data-ttu-id="5f989-355">Регистрация выполняется на странице AppRegNew.aspx любого веб-сайта SharePoint в подписке на Office 365.</span><span class="sxs-lookup"><span data-stu-id="5f989-355">You perform the registration on the AppRegNew.aspx page of any SharePoint website in the Office 365 subscription.</span></span> <span data-ttu-id="5f989-356">Подробные сведения см. в статье [Регистрация надстроек SharePoint](register-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="5f989-356">For details, see [Register SharePoint Add-ins](register-sharepoint-add-ins.md).</span></span> 
  
  <span data-ttu-id="5f989-357">В рамках этого процесса вы получаете новые идентификатор и секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="5f989-357">As part of this process, you obtain a new Client ID and Client Secret.</span></span> <span data-ttu-id="5f989-358">Вставьте эти значения в файле web.config для ключей **ClientId** (не **ida:ClientID**) и **ClientSecret**.</span><span class="sxs-lookup"><span data-stu-id="5f989-358">Insert these values in the web.config for the **ClientId** (not **ida:ClientID**) and **ClientSecret** keys.</span></span>
    
  > [!WARNING] 
  > <span data-ttu-id="5f989-359">Если по той или иной причине вы нажмете клавишу F5 после внесения этого изменения, то Инструменты разработчика Office для Visual Studio заменят одно из этих значений или оба.</span><span class="sxs-lookup"><span data-stu-id="5f989-359">If for any reason you select F5 after making this change, the Office Developer Tools for Visual Studio overwrites one or both of these values.</span></span> <span data-ttu-id="5f989-360">По этой причине следует записывать значения, полученные на странице AppRegNew.aspx, и всегда проверять значения в файле web.config непосредственно перед публикацией приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5f989-360">Caution  If for any reason you press F5 after making this change, the Office Developer Tools for Visual Studio will overwrite one or both of these values. For that reason, you should keep a record of the values obtained with AppRegNew.aspx and always verify that the values in the web.config are correct just before you publish the ASP.NET application.</span></span> 

### <a name="publish-the-aspnet-application-to-azure-and-install-the-add-in-to-sharepoint"></a><span data-ttu-id="5f989-361">Публикация приложения ASP.NET в Azure и установка надстройки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f989-361">Publish the ASP.NET application to Azure and install the add-in to SharePoint</span></span>

1. <span data-ttu-id="5f989-362">Опубликовать приложение ASP.NET на веб-сайте Azure можно несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="5f989-362">There are several ways to publish an ASP.NET application to an Azure Web Site. For more information, see  How to Deploy an Azure Web Site.</span></span> <span data-ttu-id="5f989-363">Дополнительные сведения см. в статье [Развертывание локального репозитория Git в службе приложений Azure](https://docs.microsoft.com/ru-RU/azure/app-service/app-service-deploy-local-git).</span><span class="sxs-lookup"><span data-stu-id="5f989-363">For more information, see [Local Git Deployment to Azure App Service](https://docs.microsoft.com/ru-RU/azure/app-service/app-service-deploy-local-git).</span></span>
    
2. <span data-ttu-id="5f989-364">В Visual Studio щелкните правой кнопкой мыши проект SharePoint и выберите команду **Упаковать**.</span><span class="sxs-lookup"><span data-stu-id="5f989-364">In Visual Studio, right-click the SharePoint Add-in project and select **Package**.</span></span> <span data-ttu-id="5f989-365">На открывшейся странице **Публикация надстройки** нажмите **Упаковать надстройку**.</span><span class="sxs-lookup"><span data-stu-id="5f989-365">On the **Publish your add-in** page, choose the **Package the add-in** button.</span></span> <span data-ttu-id="5f989-366">Откроется проводник с папкой, содержащей пакет надстройки.</span><span class="sxs-lookup"><span data-stu-id="5f989-366">File Explorer opens to the folder with the add-in package.</span></span>    
 
3. <span data-ttu-id="5f989-367">Войдите в Office 365 от имени глобального администратора и перейдите к семейству веб-сайтов с каталогом надстроек организации.</span><span class="sxs-lookup"><span data-stu-id="5f989-367">Sign in to Office 365 as a global administrator, and navigate to the organization add-in catalog site collection.</span></span> <span data-ttu-id="5f989-368">(Если такого семейства нет, создайте его.</span><span class="sxs-lookup"><span data-stu-id="5f989-368">(If there isn't one, create it.</span></span> <span data-ttu-id="5f989-369">См. статью [Использование каталога приложений для развертывания пользовательских бизнес-приложений в среде SharePoint Online](https://support.office.com/en-us/article/Use-the-App-Catalog-to-make-custom-business-apps-available-for-your-SharePoint-Online-environment-0b6ab336-8b83-423f-a06b-bcc52861cba0?CorrelationId=40e9dc6b-213e-4496-8c5f-40ca27922fa1&ui=en-US&rs=en-US&ad=US&ocmsassetID=HA102772362).)</span><span class="sxs-lookup"><span data-stu-id="5f989-369">Login to Office 365 as a global administrator, and navigate to the organization add-in catalog site collection. (If there isn't one, create it. See  [Use the Add-in Catalog to make custom business add-ins available for your SharePoint Online environment](https://support.office.com/en-us/article/Use-the-App-Catalog-to-make-custom-business-apps-available-for-your-SharePoint-Online-environment-0b6ab336-8b83-423f-a06b-bcc52861cba0?CorrelationId=40e9dc6b-213e-4496-8c5f-40ca27922fa1&ui=en-US&rs=en-US&ad=US&ocmsassetID=HA102772362).)</span></span>    
 
4. <span data-ttu-id="5f989-370">Отправьте пакет надстройки в каталог надстроек.</span><span class="sxs-lookup"><span data-stu-id="5f989-370">Upload the add-in package to the add-in catalog.</span></span>    
 
5. <span data-ttu-id="5f989-371">Откройте на любом сайте подписки страницу **Контент сайта** и нажмите **Добавить надстройку**.</span><span class="sxs-lookup"><span data-stu-id="5f989-371">Navigate to the  **Site Contents** page of any website in the subscription and click **add an add-in**.</span></span>    
 
6. <span data-ttu-id="5f989-372">На странице **Надстройки** найдите раздел **Надстройки, которые вы можете добавить** и выберите значок вашей надстройки.</span><span class="sxs-lookup"><span data-stu-id="5f989-372">On the  **Your Add-ins** page, scroll to the **Add-ins you can add** section and click the icon for your add-in.</span></span>    
 
7. <span data-ttu-id="5f989-373">После установки надстройки щелкните ее значок на странице **Контент сайта**, чтобы запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="5f989-373">After the add-in has installed, click it's icon on the  **Site Contents** page to launch the add-in.</span></span>    
 
<span data-ttu-id="5f989-374">Дополнительные сведения об установке надстроек SharePoint см. в статье [Развертывание и установка надстроек SharePoint: методы и параметры](deploying-and-installing-sharepoint-add-ins-methods-and-options.md).</span><span class="sxs-lookup"><span data-stu-id="5f989-374">For more information about installing SharePoint Add-ins, see  [Deploying and installing SharePoint Add-ins: methods and options](deploying-and-installing-sharepoint-add-ins-methods-and-options.md).</span></span>
 

## <a name="deploy-the-add-in-to-production"></a><span data-ttu-id="5f989-375">Развертывание надстройки в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="5f989-375">Deploying the add-in to production</span></span>

<span data-ttu-id="5f989-376">Завершив тестирование, вы можете развернуть надстройку в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5f989-376">When you have finished all testing you can deploy the add-in in production. This may require some changes.</span></span> <span data-ttu-id="5f989-377">Для этого может потребоваться внести некоторые изменения.</span><span class="sxs-lookup"><span data-stu-id="5f989-377">This may require some changes.</span></span>

1. <span data-ttu-id="5f989-378">Если рабочий домен приложения ASP.NET отличается от промежуточного домена, необходимо изменить значение **AppRedirectUrl** в файле web.config и значение **StartPage** в файле AppManifest.xml, а затем заново упаковать надстройку SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5f989-378">If the production domain of the ASP.NET application is different from the staging domain, you will have to change  **AppRedirectUrl** value in the web.config and the **StartPage** value in the AppManifest.xml file, and repackage the SharePoint Add-in. See the procedure Modify the code and markup in the application above.</span></span> <span data-ttu-id="5f989-379">См. раздел [Изменение кода и разметки в приложении](#to-modify-the-code-and-markup-in-the-application) ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5f989-379">See the procedure [To modify the code and markup in the application](#to-modify-the-code-and-markup-in-the-application) earlier in this article.</span></span>    
 
2. <span data-ttu-id="5f989-380">При изменении домена также необходимо изменить регистрационные данные надстроек в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f989-380">The change in domain also requires that you edit the add-ins registration with Azure AD.</span></span> <span data-ttu-id="5f989-381">См. раздел [Изменение регистрационных данных в Azure AD и регистрация надстройки в службе контроля доступа](#to-modify-the-azure-ad-registration-and-register-the-add-in-with-acs) ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5f989-381">See the procedure [To modify the Azure AD registration and register the add-in with ACS](#to-modify-the-azure-ad-registration-and-register-the-add-in-with-acs) earlier in this article.</span></span>    
 
3. <span data-ttu-id="5f989-382">Как упоминается в том же разделе, при изменении домена также требуется повторная регистрация надстройки в ACS (и службе управления надстройками для подписки).</span><span class="sxs-lookup"><span data-stu-id="5f989-382">The change in domain also requires that you re-register the add-in with ACS (and the subscription's Add-in Management Service) as described in the same procedure.</span></span> <span data-ttu-id="5f989-383">*Изменить* регистрационные данные надстройки в ACS невозможно. Однако создавать новые идентификатор и секрет клиента на странице AppRegNew.aspx необязательно.</span><span class="sxs-lookup"><span data-stu-id="5f989-383">(There is no way to *edit* an add-in's registration with ACS.) However, it is not necessary to generate a new Client ID or Client Secret on the AppRegNew.aspx page.</span></span> <span data-ttu-id="5f989-384">Вы можете скопировать исходные значения ключей **ClientId** (не **ida:ClientID**) и **ClientSecret** из файла web.config в новую форму AppRegNew.</span><span class="sxs-lookup"><span data-stu-id="5f989-384">You can copy the original values from the **ClientId** (not **ida:ClientID**) and **ClientSecret** keys of the web.config into the AppRegNew form.</span></span> <span data-ttu-id="5f989-385">*Если вы все же создаете новые значения, обязательно скопируйте их в ключи в файле web.config.*</span><span class="sxs-lookup"><span data-stu-id="5f989-385">*If you do generate new ones, be sure to copy the new values to the keys in web.config.*</span></span> 
    
 
## <a name="see-also"></a><span data-ttu-id="5f989-386">См. также</span><span class="sxs-lookup"><span data-stu-id="5f989-386">See also</span></span>

- [<span data-ttu-id="5f989-387">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="5f989-387">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)