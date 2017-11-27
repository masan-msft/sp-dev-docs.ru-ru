---
title: "Создание мобильного приложения в SharePoint, который содержит данные из внешнего источника данных"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f1d62256-aca0-4a59-8145-0add9e68a449
ms.openlocfilehash: 9a76bf3a652e116d175227e9dff7563c8cd0e327
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="create-a-mobile-app-in-sharepoint-that-contains-data-from-an-external-data-source"></a><span data-ttu-id="85894-102">Создание мобильного приложения в SharePoint, который содержит данные из внешнего источника данных</span><span class="sxs-lookup"><span data-stu-id="85894-102">Create a mobile app in SharePoint that contains data from an external data source</span></span>

<span data-ttu-id="85894-103">Узнайте, как создать простое приложение мобильных устройств в SharePoint, который содержит данные из внешнего источника данных с помощью служб Business Connectivity Services, подключение к внешнему списку.</span><span class="sxs-lookup"><span data-stu-id="85894-103">Learn how to create a simple mobile app in SharePoint that contains data from external data source by using Business Connectivity Services and connecting to an external list.</span></span>
<span data-ttu-id="85894-104">SharePoint позволяет создавать приложения для мобильных устройств, имеющие доступ к внешним данным из баз данных, корпоративных приложений и служб Web 2.0, с помощью служб Business Connectivity Services.</span><span class="sxs-lookup"><span data-stu-id="85894-104">SharePoint enables you to build mobile applications that can access external data from databases, enterprise applications, and Web 2.0 services using Business Connectivity Services.</span></span> <span data-ttu-id="85894-105">Можно также указать полный взаимодействия с внешними данными, включая возможностью обратной записи с мобильного устройства.</span><span class="sxs-lookup"><span data-stu-id="85894-105">You can also provide complete interaction with the external data including write-back capabilities from your mobile device.</span></span> <span data-ttu-id="85894-106">Это делается путем создания приложения, которые подключаются к внешним спискам, которые представляют собой особый тип списков в SharePoint, которые основаны на внешние типы контента и содержат данные из внешней системы.</span><span class="sxs-lookup"><span data-stu-id="85894-106">You do this by creating apps that connect to external lists, which are a special type of lists in SharePoint that are based on external content types and contain data from an external system.</span></span> <span data-ttu-id="85894-107">Новый шаблон списка SharePoint для Windows Phone в Visual Studio 2010 позволяет вам быстро и легко создавать приложения для Windows Phone, которое подключается к внешним спискам.</span><span class="sxs-lookup"><span data-stu-id="85894-107">The new Windows Phone SharePoint List template in Visual Studio 2010 Express enables you to quickly and easily create apps for the Windows Phone that connects to external lists.</span></span> <span data-ttu-id="85894-108">Например можно создавать приложения для Windows phone, которое переводит каталог продуктов для список в SharePoint на номер телефона для сотрудников отдела продаж.</span><span class="sxs-lookup"><span data-stu-id="85894-108">For example, you can build a Windows phone app that brings the product catalog for an inventory list in SharePoint to the phone for the sales people.</span></span> <span data-ttu-id="85894-109">В этом разделе показано, как создать приложение Windows Phone, которое отображает внешних данных из учебной базы данных "Борей" с помощью подключения к внешнему списку в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="85894-109">This topic shows how to create a Windows Phone app that displays external data from the Northwind sample database by connecting to an external list in SharePoint.</span></span> <span data-ttu-id="85894-110">Обратите внимание на то, что в этом примере внешний список подключается к базе данных Northwind, с помощью настраиваемой службы OData; Тем не менее можно подключиться к непосредственно баз данных, а также все внешние системы, поддерживаемый Business Connectivity Services с помощью внешних списков.</span><span class="sxs-lookup"><span data-stu-id="85894-110">Notice that in this example, the external list connects to the Northwind database using a custom OData service; however, it's possible to connect to databases directly as well as any external system that is supported by Business Connectivity Services, using external lists.</span></span> <span data-ttu-id="85894-111">С помощью нового шаблона списка SharePoint в Visual Studio можно создать мобильного приложения, который можно получить доступ к внешнему списку на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="85894-111">With the new SharePoint List template in Visual Studio, you can create a mobile app that can access an external list on a SharePoint site.</span></span> <span data-ttu-id="85894-112">В этой статье приводятся пошаговые процедуры, которая начинается с Отправка внешних модели службы подключения к бизнес-данных (BDC) и заканчивается на тестирование нового мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="85894-112">This article provides a step-by-step procedure that begins with uploading an external Business Data Connectivity (BDC) service model and ends with testing your new mobile app.</span></span>
  
    
    


> <span data-ttu-id="85894-113">**Важные:** При разработке приложения для Windows Phone 8, должны использовать Visual Studio Express 2012 г., а не в Visual Studio 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="85894-113">**Important:** If you are developing an app for Windows Phone 8, you must use Visual Studio Express 2012 instead of Visual Studio 2010 Express.</span></span> <span data-ttu-id="85894-114">За исключением среды разработки все сведения в этой статье применимы к созданию приложений для Windows Phone 8 и Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="85894-114">Except for the development environment, all information in this article applies to creating apps for both Windows Phone 8 and Windows Phone 7.</span></span> <span data-ttu-id="85894-115">> Для получения дополнительных сведений см [как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="85894-115">> For more information, see  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span></span> 
  
    
    


## <a name="prerequisites-for-creating-a-mobile-app-that-contains-external-data"></a><span data-ttu-id="85894-116">Необходимые условия для создания мобильного приложения, которое содержит внешние данные</span><span class="sxs-lookup"><span data-stu-id="85894-116">Prerequisites for creating a mobile app that contains external data</span></span>
<span data-ttu-id="85894-117"><a name="SP15Createmobileapp_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="85894-117"></span></span>


- <span data-ttu-id="85894-118">Для установки SharePoint с правами администратора для загрузки модели BDC для базы данных Northwind и сайта SharePoint, где вы создаете внешний список</span><span class="sxs-lookup"><span data-stu-id="85894-118">A SharePoint installation with administrative privileges to upload the BDC model for the Northwind database and a SharePoint site where you create the external list</span></span>
    
  
- <span data-ttu-id="85894-119">Microsoft Visual Studio Express с новыми шаблонами телефонов SharePoint из [Пакета SDK Microsoft SharePoint для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)</span><span class="sxs-lookup"><span data-stu-id="85894-119">Microsoft Visual Studio Express with the new SharePoint phone templates from  [Microsoft SharePoint SDK for Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)</span></span>
    
  
- <span data-ttu-id="85894-120">Модели BDC для нашего exampleNorthwind_oData.bdmc (загрузить из [SharePoint: создание простой внешний список телефонных приложения](http://code.msdn.microsoft.com/sharepoint/SharePoint-Create-a-88800202))</span><span class="sxs-lookup"><span data-stu-id="85894-120">The BDC model for our exampleNorthwind_oData.bdmc (download from  [SharePoint: Create a simple external list-based phone app](http://code.msdn.microsoft.com/sharepoint/SharePoint-Create-a-88800202))</span></span>
    
  
- <span data-ttu-id="85894-121">Для установки SharePoint с правами администратора для загрузки модели BDC для базы данных Northwind и сайта SharePoint, где вы создаете внешний список</span><span class="sxs-lookup"><span data-stu-id="85894-121">A SharePoint installation with administrative privileges to upload the BDC model for the Northwind database and a SharePoint site where you create the external list</span></span>
    
  

## <a name="step-1-upload-a-bdc-metadata-model"></a><span data-ttu-id="85894-122">Шаг 1: Отправка метаданных модели BDC</span><span class="sxs-lookup"><span data-stu-id="85894-122">Step 1: Upload a BDC metadata model</span></span>
<span data-ttu-id="85894-123"><a name="HowToCreateSimpleExternalListBasedPhoneApp_Step1"> </a></span><span class="sxs-lookup"><span data-stu-id="85894-123"></span></span>

<span data-ttu-id="85894-p103">Модели BDC  это основной Business Connectivity Services. Это XML-файл, использующий структур данных, таких как **сущности** (внешнего типа контента) и **метод** для абстрактного сложных сведения о внешней системе. Он будет создан при создании внешнего типа контента с помощью SharePoint Designer и для некоторых типов данных такие источники .NET и OData, вам необходимо создать модель BDC вручную или с помощью Visual Studio. При отправке модели BDC в хранилище метаданных BDC, с помощью центра администрирования SharePoint внешних типов контента, определенных в модели можно использовать для создания внешних списков в SharePoint, которые представляют списки, отображающие данные из связанного внешней системы. На этом этапе будет передачи данных "Борей" пример BDC модели в хранилище метаданных с помощью центра администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="85894-p103">A BDC model is the core of Business Connectivity Services. It's an XML file that uses data structures such as **Entity** (external content type) and **Method** to abstract out complex details about the external system. It's auto-generated when you create an external content type using SharePoint Designer and for some data source types such .NET and OData sources, you need to create the BDC model manually or by using Visual Studio. When you upload a BDC model to the BDC metadata store using SharePoint Central Administration, the external content types defined in the model can be used to create external lists in SharePoint which are lists that display data from the underlying external system. In this step, you'll upload the Northwind sample BDC model to the Metadata Store using SharePoint Central Administration.</span></span>
  
    
    

1. <span data-ttu-id="85894-129">Перейдите в центр администрирования.</span><span class="sxs-lookup"><span data-stu-id="85894-129">Navigate to Central Administration.</span></span>
    
  
2. <span data-ttu-id="85894-130">Выберите **Управление приложениями**, а затем выберите **Управление приложениями-службами**.</span><span class="sxs-lookup"><span data-stu-id="85894-130">Choose **Application Management**, and then choose **Manage Service Applications**.</span></span>
    
  
3. <span data-ttu-id="85894-131">На странице приложения-службы выберите **Службы подключения к бизнес-данным**.</span><span class="sxs-lookup"><span data-stu-id="85894-131">On the Service Application page, choose **Business Data Connectivity Service**.</span></span>
    
  
4. <span data-ttu-id="85894-132">На ленте в приложении-службе BDC выберите команду **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="85894-132">On the ribbon in the BDC Service application, choose **Import**.</span></span>
    
  
5. <span data-ttu-id="85894-133">На странице "Импорт модели BDC" выберите **Служба подключения к бизнес-данным**.</span><span class="sxs-lookup"><span data-stu-id="85894-133">On the Import BDC Model page, choose **Business Data Connectivity Service**.</span></span>
    
  
6. <span data-ttu-id="85894-134">На ленте в приложении-службе BDC выберите команду **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="85894-134">On the ribbon in the BDC Service application, choose **Import**.</span></span>
    
  
7. <span data-ttu-id="85894-135">На странице "Импорт модели BDC" нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="85894-135">On the Import BDC Model page, choose **Browse**.</span></span>
    
  
8. <span data-ttu-id="85894-136">В диалоговом окне **выбрать файл для загрузки** перейдите к файлу Northwind_oData.bdcm и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="85894-136">In the **Choose a File to upload** dialog box, browse to the Northwind_oData.bdcm file, and then choose **Open**.</span></span>
    
  
9. <span data-ttu-id="85894-137">После импорта файла нажмите кнопку « **ОК** ».</span><span class="sxs-lookup"><span data-stu-id="85894-137">After the file is imported, choose the **OK** button.</span></span>
    
  

## <a name="step-2-grant-permissions"></a><span data-ttu-id="85894-138">Шаг 2: Предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="85894-138">Step 2: Grant permissions</span></span>
<span data-ttu-id="85894-139"><a name="HowToCreateSimpleExternalListBasedPhoneApp_Step2"> </a></span><span class="sxs-lookup"><span data-stu-id="85894-139"></span></span>

<span data-ttu-id="85894-p104">Далее необходимо задать разрешения для модели BDC, чтобы указать, кто может выполнять методы, описанные в этой модели. Этот шаг является обязательным. Рекомендуется предоставить определенные разрешения для каждого пользователя или группы, которое должно их, таким образом, что учетные данные полностью предоставления минимальных прав, необходимых для выполнения необходимых задач. Дополнительные сведения о настройке разрешений см служба подключения к бизнес разрешения в  [Общие сведения о безопасности служб Business Connectivity Services (SharePoint Server 2010)](http://technet.microsoft.com/en-us/library/ee661740.aspx). На этом этапе предоставить разрешение на свой адрес выполнение методов, описанных в модели BDC образец данных "Борей".</span><span class="sxs-lookup"><span data-stu-id="85894-p104">Next you need to set permissions on the BDC model to specify who can execute the methods described in the model. This is a required step. We recommend that you give specific permissions to each user or group that needs them, in such a way that the credentials provide the least privilege necessary to perform the needed tasks. For more information about setting permissions, see Business Connectivity Service permissions overview in  [Business Connectivity Services security overview (SharePoint Server 2010)](http://technet.microsoft.com/en-us/library/ee661740.aspx). In this step, you give permission to yourself to execute the methods described in the Northwind sample BDC model.</span></span>
  
    
    

1. <span data-ttu-id="85894-145">Перейдите в центр администрирования.</span><span class="sxs-lookup"><span data-stu-id="85894-145">Navigate to Central Administration.</span></span>
    
  
2. <span data-ttu-id="85894-146">Выберите **Управление приложениями**, а затем выберите **Управление приложениями-службами**.</span><span class="sxs-lookup"><span data-stu-id="85894-146">Choose **Application Management**, and then choose **Manage Service Applications**.</span></span>
    
  
3. <span data-ttu-id="85894-147">На странице приложения-службы выберите **Службы подключения к бизнес-данным**.</span><span class="sxs-lookup"><span data-stu-id="85894-147">On the Service Application page, choose **Business Data Connectivity Service**.</span></span>
    
  
4. <span data-ttu-id="85894-148">На ленте выберите из раскрывающегося списка в группе **представление** **Моделей BDC**.</span><span class="sxs-lookup"><span data-stu-id="85894-148">In the ribbon, choose **BDC Models** from the drop-down list in the **View** group.</span></span>
    
  
5. <span data-ttu-id="85894-149">В списке моделей BDC наведите указатель мыши на Northwind_oData.bdcm и выберите команду **Задать разрешения**, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="85894-149">In the list of BDC models, hover over Northwind_oData.bdcm and choose **Set Permissions**, as shown in Figure 1.</span></span>
    
   <span data-ttu-id="85894-150">**На рисунке 1. Выбор разрешений для модели BDC**</span><span class="sxs-lookup"><span data-stu-id="85894-150">**Figure 1. Choosing permissions for BDC model**</span></span>

  

  ![Выбор разрешений для модели подключения к бизнес-данным](../images/SPCon15_BDC_SetPermissions_ODataWebNorthWind.png)
  

  

  
6. <span data-ttu-id="85894-152">В диалоговом окне **Задать разрешения для объекта** нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="85894-152">In the **Set Object Permissions** dialog box, choose the **Browse** button.</span></span>
    
  
7. <span data-ttu-id="85894-153">В диалоговом окне **Выбор пользователей и групп** выполните поиск учетной записи и нажмите кнопку « **ОК** ».</span><span class="sxs-lookup"><span data-stu-id="85894-153">In the **Select People and Groups** dialog box, search for your account and choose the **OK** button.</span></span>
    
  
8. <span data-ttu-id="85894-154">Выберите разрешения для **редактирования**, **выполнение**, **Доступно для выбора в клиентах** и **Задание разрешений**, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="85894-154">Select the permissions for **Edit**, **Execute**, **Selectable In Clients**, and **Set Permissions**, as shown in Figure 2.</span></span>
    
   <span data-ttu-id="85894-155">**На рисунке 2. Настройка разрешений объектов**</span><span class="sxs-lookup"><span data-stu-id="85894-155">**Figure 2. Setting object permissions**</span></span>

  

  ![Установка разрешений для объекта подключения к бизнес-данным](../images/SPCon15_Setting_BDCObjectPermission_DialogueBox.png)
  

  

  
9. <span data-ttu-id="85894-157">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="85894-157">Choose the **OK** button.</span></span>
    
  
10. <span data-ttu-id="85894-158">На ленте выберите **Внешние типы контента** из раскрывающегося списка в группе **представление**.</span><span class="sxs-lookup"><span data-stu-id="85894-158">In the ribbon, select **External Content Types** from the drop-down list in the **View** group.</span></span>
    
  
11. <span data-ttu-id="85894-159">В списке внешние типы контента наведите указатель мыши на **клиента** и выберите **Задание разрешений**.</span><span class="sxs-lookup"><span data-stu-id="85894-159">In the list of external content types, hover over **Customer**, and then choose **Set Permissions**.</span></span>
    
  
12. <span data-ttu-id="85894-160">В диалоговом окне **Задать разрешения для объекта** нажмите кнопку **Обзор** и поиска для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="85894-160">In the **Set Object Permissions** dialog box, choose the **Browse** button and search for your account.</span></span>
    
  
13. <span data-ttu-id="85894-161">В диалоговом окне **Задать разрешения для объекта** последовательно выберите пункты **Добавить** и выберите разрешения для **редактирования**, **выполнение**, **Доступно для выбора в клиентах** и **Задание разрешений**.</span><span class="sxs-lookup"><span data-stu-id="85894-161">In the **Set Object Permissions** dialog box, choose **Add** and select the permissions for **Edit**, **Execute**, **Selectable In Clients**, and **Set Permissions**.</span></span>
    
  
14. <span data-ttu-id="85894-162">Убедитесь, что установлен флажок **Распространить разрешения**.</span><span class="sxs-lookup"><span data-stu-id="85894-162">Ensure that the **Propagate Permissions** box is selected.</span></span>
    
  
15. <span data-ttu-id="85894-163">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="85894-163">Choose the **OK** button.</span></span>
    
  

## <a name="step-3-create-an-external-list"></a><span data-ttu-id="85894-164">Шаг 3: Создание внешнего списка</span><span class="sxs-lookup"><span data-stu-id="85894-164">Step 3: Create an external list</span></span>
<span data-ttu-id="85894-165"><a name="HowToCreateSimpleExternalListBasedPhoneApp_Step3"> </a></span><span class="sxs-lookup"><span data-stu-id="85894-165"></span></span>

<span data-ttu-id="85894-p105">Теперь, когда отправлен модели BDC и установка разрешений, можно создать внешний список на основе внешнего типа контента, определенных в модели BDC. На этом этапе создается внешний список на основе клиента внешнего типа контента определенных в модели Northwind BDC, загруженный в  [Шаг 1: Отправка метаданных модели BDC](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md#HowToCreateSimpleExternalListBasedPhoneApp_Step1).</span><span class="sxs-lookup"><span data-stu-id="85894-p105">Now that you've uploaded the BDC model and set permissions, you can create an external list based on the external content type defined in the BDC model. In this step, you will create an external list based on the Customer external content type defined in the Northwind BDC model you uploaded in  [Step 1: Upload a BDC metadata model](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md#HowToCreateSimpleExternalListBasedPhoneApp_Step1).</span></span>
  
    
    

1. <span data-ttu-id="85894-168">Перейдите на сайт SharePoint, где будут нового списка.</span><span class="sxs-lookup"><span data-stu-id="85894-168">Navigate to the SharePoint site where you want the new list.</span></span>
    
  
2. <span data-ttu-id="85894-169">На домашней странице веб-узла выберите **Дополнительные**.</span><span class="sxs-lookup"><span data-stu-id="85894-169">On the home page of the site, choose **More**.</span></span>
    
  
3. <span data-ttu-id="85894-170">На странице "приложения" выберите **Добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="85894-170">On the Apps page, choose **Add an App**.</span></span>
    
  
4. <span data-ttu-id="85894-171">На странице Добавить страницу приложения наведите указатель мыши на **Внешний список** и выберите команду **добавить его**.</span><span class="sxs-lookup"><span data-stu-id="85894-171">On the Add an App page, hover over **External List** and choose **Add it**.</span></span>
    
  
5. <span data-ttu-id="85894-172">В диалоговом окне **Добавление внешнего списка** введите имя, напримерклиентов в поле **имя**.</span><span class="sxs-lookup"><span data-stu-id="85894-172">In the **Adding an External List** dialog box, enter a name such asCustomers in the **Name** field.</span></span>
    
  
6. <span data-ttu-id="85894-173">В поле **Внешний тип контента** укажите источник внешних данных, который загрузил на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="85894-173">In the **External Content Type** box, specify the external data source that you uploaded in step 1.</span></span>
    
  
7. <span data-ttu-id="85894-174">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="85894-174">Choose the **OK** button.</span></span>
    
  
8. <span data-ttu-id="85894-175">На странице "приложения" выберите **Список клиентов** для просмотра списка.</span><span class="sxs-lookup"><span data-stu-id="85894-175">On the Apps page, choose **Customers List** to view the list.</span></span>
    
  

## <a name="step-4-create-a-mobile-app-using-the-windows-phone-sharepoint-list-application-template"></a><span data-ttu-id="85894-176">Шаг 4: Создание мобильного приложения на основе шаблона приложения списка SharePoint для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="85894-176">Step 4: Create a mobile app using the Windows Phone SharePoint List Application template</span></span>
<span data-ttu-id="85894-177"><a name="HowToCreateSimpleExternalListBasedPhoneApp_Step4"> </a></span><span class="sxs-lookup"><span data-stu-id="85894-177"></span></span>

<span data-ttu-id="85894-178">Внешний список готов, и теперь можно создать приложение Windows Phone 7, которое подключается к внешнему списку, созданной на  [Шаг 3: Создание внешнего списка](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md#HowToCreateSimpleExternalListBasedPhoneApp_Step3) и отображения данных клиента из базы данных Northwind.</span><span class="sxs-lookup"><span data-stu-id="85894-178">Your external list is ready and you can now create a Windows Phone 7 app that connects to the external list you created in  [Step 3: Create an external list](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md#HowToCreateSimpleExternalListBasedPhoneApp_Step3) and display Customer data from the Northwind database.</span></span>
  
    
    

1. <span data-ttu-id="85894-179">Запустите Visual Studio 2010, экспресс-выпуск.</span><span class="sxs-lookup"><span data-stu-id="85894-179">Start Visual Studio 2010 Express.</span></span>
    
  
2. <span data-ttu-id="85894-p106">В строке меню щелкните **файл**, **Создать проект**. Откроется диалоговое окно **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="85894-p106">On the menu bar, choose **File**, **New Project**. The **New Project** dialog box opens.</span></span>
    
  
3. <span data-ttu-id="85894-182">В диалоговом окне **Создать проект** выберите **Visual C#**, выберите **Silverlight для Windows Phone** и затем выберите **Приложения списка SharePoint для Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="85894-182">In the **New Project** dialog box, choose **Visual C#**, choose **Silverlight for Windows Phone**, and then choose **Windows Phone SharePoint List Application**.</span></span>
    
  
4. <span data-ttu-id="85894-p107">Укажите имя для проекта. В этом примере используется CustomerApp как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="85894-p107">Specify a name for the project. We use CustomerApp in this example, as shown in Figure 3.</span></span>
    
   <span data-ttu-id="85894-185">**На рисунке 3. Выбор шаблона приложения списка SharePoint для Windows Phone в Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="85894-185">**Figure 3. Selecting the Windows Phone SharePoint List Application template in Visual Studio**</span></span>

  

  ![Шаблон мобильного приложения списка SharePoint](../images/SP15Con_VisualStudioMobileSPListTemplate.png)
  

  

  
5. <span data-ttu-id="85894-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="85894-187">Choose the **OK** button.</span></span>
    
  
6. <span data-ttu-id="85894-188">В окне **Мастера приложений для телефона SharePoint** введите URL-адрес сайта SharePoint, в котором вы создали внешнего списка.</span><span class="sxs-lookup"><span data-stu-id="85894-188">In the **SharePoint Phone Application Wizard**, enter the URL of the SharePoint site in which you created the external list.</span></span>
    
  
7. <span data-ttu-id="85894-189">Выберите в списке **клиентов** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="85894-189">Choose the **Customers** list, and choose **Next**.</span></span>
    
  
8. <span data-ttu-id="85894-190">На экране **Выбор представления** выберите **Клиента чтение списка** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="85894-190">On the **Choose Views** screen, select **Customer Read List** and choose **Next**.</span></span>
    
  
9. <span data-ttu-id="85894-191">На экране **Выбор операции** выберите **отображения** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="85894-191">On the **Choose Operations** screen, choose **Display**, and then choose **Next**.</span></span>
    
  
10. <span data-ttu-id="85894-192">На экране **Выбор поля** выберите поля, которые требуется использовать или отображать в мобильного приложения и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="85894-192">On the **Choose Fields** screen, select the fields you want to use or display in your mobile app, and then choose **Next**.</span></span>
    
  
11. <span data-ttu-id="85894-193">На экране **Поля заказа** изменить порядок полей, если необходимо и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="85894-193">On the **Order Fields** screen, reorder the fields if needed, and then choose **Finish**.</span></span>
    
  
12. <span data-ttu-id="85894-194">Теперь успешно ли создан приложение, которое подключается к внешнему списку.</span><span class="sxs-lookup"><span data-stu-id="85894-194">You've now successfully created the app that connects to the external list.</span></span>
    
  

## <a name="run-and-test-your-app"></a><span data-ttu-id="85894-195">Запуск и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="85894-195">Run and test your app</span></span>
<span data-ttu-id="85894-196"><a name="HowToCreateSimpleExternalListBasedPhoneApp_RunAndTest"> </a></span><span class="sxs-lookup"><span data-stu-id="85894-196"></span></span>

<span data-ttu-id="85894-197">Теперь, когда приложение будет готово для запуска, можно проверить его использование эмулятора телефона.</span><span class="sxs-lookup"><span data-stu-id="85894-197">Now that the app is ready to run, you can test it using phone emulator.</span></span>
  
    
    

1. <span data-ttu-id="85894-198">В Visual Studio выберите **Отладка** и затем выберите команду **Начать отладку** или нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="85894-198">In Visual Studio, choose **Debug**, and then choose **Start Debugging**, or press F5.</span></span>
    
  
2. <span data-ttu-id="85894-p108">При появлении запроса вход с помощью же имя пользователя и пароль, который использовался для входа на сайт SharePoint. Убедитесь, что у вас есть права администратора.</span><span class="sxs-lookup"><span data-stu-id="85894-p108">When prompted, log in by using the same username and password that you used to log in to the SharePoint site. Ensure that you have admin rights.</span></span>
    
  
3. <span data-ttu-id="85894-201">Просмотрите этот список клиентов, как показано на рисунке 4.</span><span class="sxs-lookup"><span data-stu-id="85894-201">Scroll through the resulting Customers list, as shown in Figure 4.</span></span>
    
   <span data-ttu-id="85894-202">**На рисунке 4. Мобильное приложение отображение внешнего списка SharePoint**</span><span class="sxs-lookup"><span data-stu-id="85894-202">**Figure 4. Mobile app displaying SharePoint external list**</span></span>

  

  ![Демонстрация мобильного приложения подключения к бизнес-данным](../images/SPCon15_BDCMobileAppDemo.png)
  

  

  

> <span data-ttu-id="85894-204">**Примечание:** При использовании мастера шаблон списка SharePoint для создания мобильного приложения для внешнего списка, имеются поля только для чтения, код, созданный с помощью мастера не позволяет пользователям создавать или изменять элементы.</span><span class="sxs-lookup"><span data-stu-id="85894-204">**Note:** When you use the SharePoint List Template wizard to create a mobile app for an external list that has read-only fields, the code that is generated by the wizard does not allow users to create or edit items.</span></span> 
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="85894-205">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="85894-205">Additional resources</span></span>
<span data-ttu-id="85894-206"><a name="SP15createmobileapp_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="85894-206"></span></span>


  
    
    

-  [<span data-ttu-id="85894-207">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="85894-207">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="85894-208">Обзор шаблонов приложений Windows Phone SharePoint в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="85894-208">Overview of Windows Phone SharePoint application templates in Visual Studio</span></span>](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md)
    
  
-  [<span data-ttu-id="85894-209">Как: Создание внешних списков в SharePoint</span><span class="sxs-lookup"><span data-stu-id="85894-209">How to: Create External Lists in SharePoint</span></span>](http://msdn.microsoft.com/en-us/library/ee558778.aspx)
    
  
-  [<span data-ttu-id="85894-210">Как: Создание приложения списка Windows Phone SharePoint</span><span class="sxs-lookup"><span data-stu-id="85894-210">How to: Create a Windows Phone SharePoint list app</span></span>](how-to-create-a-windows-phone-sharepoint-list-app.md)
    
  
-  [<span data-ttu-id="85894-211">Как: Настройка среды разработки мобильных приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="85894-211">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="85894-212">Пакет SDK для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="85894-212">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="85894-213">Пакет SDK Microsoft SharePoint для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="85894-213">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

