
# <a name="publish-sharepoint-add-ins"></a><span data-ttu-id="f1c74-101">Публикация надстроек для SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1c74-101">Publish SharePoint Add-ins</span></span>
<span data-ttu-id="f1c74-102">Здесь вы найдете статьи и ресурсы, которые помогут вам публиковать свои надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f1c74-102">Find articles and resources to help you publish your SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="f1c74-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="f1c74-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="get-started-with-publishing-your-add-ins"></a><span data-ttu-id="f1c74-106">Начало работы по публикации надстроек</span><span class="sxs-lookup"><span data-stu-id="f1c74-106">Get started with publishing your add-ins</span></span>
<span data-ttu-id="f1c74-107"><a name="bk_gettingstarted"> </a></span><span class="sxs-lookup"><span data-stu-id="f1c74-107"></span></span>

<span data-ttu-id="f1c74-p102">Завершив разработку надстройки Надстройка SharePoint, нужно сделать её доступной для пользователей. Вы можете сделать это путем публикации надстройки в одном из двух мест:</span><span class="sxs-lookup"><span data-stu-id="f1c74-p102">You've finished developing your SharePoint Add-in—the final step is making that add-in available to your users. You can do this by publishing the add-in to one of two places:</span></span>
 

 

-  <span data-ttu-id="f1c74-p103">**Общедоступный Магазин Office.** Опубликуйте свою надстройку в Магазин Office, чтобы сделать ее общедоступной. Ее смогут получить пользователи любого развертывания SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f1c74-p103">**The public Office Store.** Publish your add-in to the Office Store to make the add-in publically available, so that it can be acquired by users of any SharePoint deployment.</span></span>
    
 
-  <span data-ttu-id="f1c74-p104">**Внутренний каталог надстроек организации.** Опубликуйте свою надстройку во внутреннем каталоге надстроек организации, размещенном на вашем развертывании SharePoint. Она будет доступна для пользователей, имеющих доступ к данному развертыванию SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f1c74-p104">**An internal organization add-in catalog.** Publish your add-ins to an internal organization add-in catalog, hosted on your SharePoint deployment, to make them available to users with access to that SharePoint deployment.</span></span>
    
 
<span data-ttu-id="f1c74-114">Сведения о том, как упаковать надстройку для публикации с помощью Visual Studio 2012, см. в статье [Публикация надстроек SharePoint с помощью Visual Studio](publish-sharepoint-add-ins-by-using-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="f1c74-114">For information about how to package your add-in for publication by using Visual Studio 2012, see  [Publish SharePoint Add-ins by using Visual Studio](publish-sharepoint-add-ins-by-using-visual-studio).</span></span>
 

 

### <a name="publishing-to-the-office-store"></a><span data-ttu-id="f1c74-115">Публикация в Магазине Office</span><span class="sxs-lookup"><span data-stu-id="f1c74-115">Publishing to the Office Store</span></span>

<span data-ttu-id="f1c74-116">Чтобы опубликовать надстройку в Магазине Office, сначала необходимо [зарегистрироваться в качестве разработчика Майкрософт](https://sellerdashboard.microsoft.com/Registration).</span><span class="sxs-lookup"><span data-stu-id="f1c74-116">To publish an add-in to the Office Store, you must first  [register as a Microsoft developer](https://sellerdashboard.microsoft.com/Registration).</span></span> 
 

 
<span data-ttu-id="f1c74-p105">При загрузке надстройки на Магазин Office для публикации, корпорация Майкрософт выполняет серию проверок, чтобы убедиться, что надстройка соответствует рекомендациям по содержанию и поведению надстроек. Например, выполняется проверка правильности и полноты разметки манифеста надстройки, также производится проверка всех пакетов решений SharePoint (WSP-файлы), которые включены в надстройку, на отсутствие недопустимых элементов или компонентов SharePoint с областью, которая является более широкой, чем веб. Пакет также проверяется на наличие нежелательного содержимого. Если пакет надстройки проходит все тесты, он будет упакован в файл и подписан корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f1c74-p105">When you upload an add-in to the Office Store for publication, Microsoft performs a series of verification checks to ensure your add-in adheres to the add-in content and behavior guidelines. For example, it checks whether the add-in manifest markup is valid and complete and verifies that any SharePoint solution packages (.wsp files) that are included in the add-in do not contain elements that aren't allowed, or SharePoint Features with a scope that is broader than Web. The package is also inspected for objectionable content. If the add-in package passes all tests, it's wrapped into a file and signed by Microsoft.</span></span>
 

 
<span data-ttu-id="f1c74-p106">Когда вы загружаете надстройку для публикации на Магазин Office, можно указать атрибуты лицензии, которую вы хотите предложить пользователям, загружающим эту надстройку. Лицензия для надстройки содержит следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="f1c74-p106">When you upload your add-in for publication on the Office Store, you can choose the terms of the license you want to offer users when they download it. Use this add-in license to decide:</span></span> 
 

 

- <span data-ttu-id="f1c74-123">Предлагаете ли вы надстройку бесплатно, для пробного использования или для покупки.</span><span class="sxs-lookup"><span data-stu-id="f1c74-123">Whether you are offering your add-in for free, trial, or for purchase.</span></span>
    
 
- <span data-ttu-id="f1c74-124">Может ли ваша надстройка быть приобретена для отдельного пользователя или для сайта.</span><span class="sxs-lookup"><span data-stu-id="f1c74-124">Whether your add-in can be acquired on a per-user or site basis.</span></span>
    
 
<span data-ttu-id="f1c74-p107">SharePoint не обеспечивает соблюдение условий лицензии на использование надстроек, а предоставляет систему лицензирования, которая позволяет включать в вашу надстройку алгоритмы для обеспечения соблюдения выбранных вами лицензионных ограничений. Например, вы можете включить в вашу надстройку код, который откроет пользователям доступ к некоторым функциям надстройки, если они имеют платную лицензию, и закроет доступ к этим функциям для пользователей с пробной лицензией. Дополнительные сведения см. в статье  [Лицензирование надстроек Office и SharePoint](http://msdn.microsoft.com/library/license-your-office-and-sharepoint-add-ins%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1c74-p107">SharePoint does not enforce license terms for add-in usage—it provides a licensing framework that lets you include code logic in your add-in to enforce whatever licensing restrictions you choose. For example, you can include code logic in your add-in that enables users to access certain add-in features if they have a paid license, but not if they have a trial license. For more information, see  [License your Office and SharePoint Add-ins](http://msdn.microsoft.com/library/license-your-office-and-sharepoint-add-ins%28Office.15%29.aspx).</span></span>
 

 

### <a name="publishing-to-an-add-in-catalog"></a><span data-ttu-id="f1c74-128">Публикация в каталоге надстроек</span><span class="sxs-lookup"><span data-stu-id="f1c74-128">Publishing to an add-in catalog</span></span>

<span data-ttu-id="f1c74-p108">Если вы создаете Надстройки SharePoint для использования в вашей компании или для конкретного корпоративного клиента, но не для широкой общественности, вы, вероятно, захотите опубликовать свою надстройку во внутреннем каталоге надстроек, размещенном на SharePoint. Каталог частных надстроек представляет собой специализированную коллекцию сайтов в веб-приложении SharePoint (или в аренде SharePoint Online), которая содержит библиотеки документов для Надстройки SharePoint и Надстройки Office. Размещение каталога в собственной коллекции сайтов облегчает работу по ограничению разрешений на доступ к каталогу для администратора веб-приложения или администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="f1c74-p108">If you're creating SharePoint Add-ins for your own company's use or a specific corporate client, instead of the general public, you'll likely want to publish your add-in to an internal add-in catalog hosted on SharePoint. A private add-in catalog is a dedicated site collection in a SharePoint web application (or a SharePoint Online tenancy) that hosts document libraries for SharePoint Add-ins and Office Add-ins. Putting the catalog into its own site collection makes it easier for the web application administrator or tenant administrator to limit permissions to the catalog.</span></span>
 

 
<span data-ttu-id="f1c74-p109">Загрузка Надстройка SharePoint в корпоративный каталог надстроек так же проста, как и загрузка любых файлов в библиотеку документов SharePoint. Необходимо заполнить всплывающую форму, в которой нужно указать местный URL-адрес пакета надстройки и другую информацию, например название надстройки. При загрузке надстроек в каталог выполняются аналогичные проверки. Надстройки, которые не проходят проверку, помечаются в каталоге как недопустимые или отключенные.</span><span class="sxs-lookup"><span data-stu-id="f1c74-p109">Uploading a SharePoint Add-in to a corporate add-in catalog is as easy as uploading any file to a SharePoint document library. You fill out a pop-up form in which you supply the local URL of the add-in package and other information, such as the name of the add-in. When you upload the add-in to an add-in catalog, there are similar checks and add-ins that do not pass are marked as invalid or disabled in the catalog.</span></span>
 

 

## <a name="deciding-where-to-publish-your-sharepoint-add-in"></a><span data-ttu-id="f1c74-135">Выбор места для публикации надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1c74-135">Deciding where to publish your SharePoint Add-in</span></span>
<span data-ttu-id="f1c74-136"><a name="bk_decide"> </a></span><span class="sxs-lookup"><span data-stu-id="f1c74-136"></span></span>

<span data-ttu-id="f1c74-p110">В следующей таблице приведены различия между публикацией в Магазин Office и каталоге надстроек, а также перечень вопросов, которые необходимо учитывать при выборе места для публикации надстройки. Мы рекомендуем определиться с местом для публикации вашей надстройки, прежде чем начинать ее проектирование и разработку. В некоторых случаях, например при лицензировании, место публикации надстройки будет влиять на проектирование и разработку вашей надстройки.</span><span class="sxs-lookup"><span data-stu-id="f1c74-p110">The following table offers a comparison of publishing to the Office Store or to an add-in catalog, and lists issues to consider when deciding where to publish your add-in. We recommend you decide where you plan to publish your add-in before you design and develop it; in some cases, such as licensing, where you publish your add-in will affect the design and development of your add-in.</span></span>
 

 

<span data-ttu-id="f1c74-139">**Таблица 1. Вопросы, которые необходимо учитывать при выборе места для публикации надстройки**</span><span class="sxs-lookup"><span data-stu-id="f1c74-139">**Table 1. Considerations for where to publish your add-in**</span></span>


|<span data-ttu-id="f1c74-140">**Магазин Office**</span><span class="sxs-lookup"><span data-stu-id="f1c74-140">**Office Store**</span></span>|<span data-ttu-id="f1c74-141">**Каталог надстроек**</span><span class="sxs-lookup"><span data-stu-id="f1c74-141">**Add-in Catalog**</span></span>|
|:-----|:-----|
|<span data-ttu-id="f1c74-142">Надстройка является общедоступной.</span><span class="sxs-lookup"><span data-stu-id="f1c74-142">Add-in is publically available.</span></span>|<span data-ttu-id="f1c74-143">Надстройка доступна для пользователей, имеющих доступ к данному развертыванию SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1c74-143">Add-in is available to users with access to this SharePoint deployment</span></span>|
|<span data-ttu-id="f1c74-144">Доступна система лицензирования.</span><span class="sxs-lookup"><span data-stu-id="f1c74-144">Licensing framework available.</span></span>|<span data-ttu-id="f1c74-145">Система лицензирования не доступна для использования.</span><span class="sxs-lookup"><span data-stu-id="f1c74-145">Licensing framework is not available for use.</span></span>|
|<span data-ttu-id="f1c74-146">Пакет надстройки проверяется корпорацией Майкрософт на предмет соблюдения политик по поведению и содержанию.</span><span class="sxs-lookup"><span data-stu-id="f1c74-146">Add-in package verified by Microsoft for technical and content adherence to policies.</span></span>|<span data-ttu-id="f1c74-147">Пакет надстройки проверяется SharePoint при загрузке надстройки.</span><span class="sxs-lookup"><span data-stu-id="f1c74-147">Add-in package verification performed by SharePoint when add-in is uploaded.</span></span>|
|<span data-ttu-id="f1c74-148">Для загрузки надстроек вы должны быть зарегистрированы на Панели мониторинга продаж Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f1c74-148">You must be signed up with Microsoft Seller Dashboard to upload add-ins.</span></span>|<span data-ttu-id="f1c74-149">Регистрация в корпорации Майкрософт не требуется.</span><span class="sxs-lookup"><span data-stu-id="f1c74-149">No registration with Microsoft required.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="f1c74-150">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f1c74-150">Additional resources</span></span>
<span data-ttu-id="f1c74-151"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f1c74-151"></span></span>


-  [<span data-ttu-id="f1c74-152">Создание и обновление идентификаторов и секретов клиентов на Панели мониторинга продаж</span><span class="sxs-lookup"><span data-stu-id="f1c74-152">Create or update client IDs and secrets in the Seller Dashboard</span></span>](http://msdn.microsoft.com/library/create-or-update-client-ids-and-secrets-in-the-seller-dashboard%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="f1c74-153">Отправка надстроек Office и SharePoint и приложений для Office 365 в Магазин Office с помощью Панели мониторинга продаж</span><span class="sxs-lookup"><span data-stu-id="f1c74-153">Use the Seller Dashboard to submit Office and SharePoint Add-ins and Office 365 apps to the Office Store</span></span>](http://msdn.microsoft.com/library/use-the-seller-dashboard-to-submit-office-and-sharepoint-add-ins-and-office-365-apps-to-the-office-store%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="f1c74-154">Политики проверки для приложений и надстроек, отправленных в Магазин Office (версия 2.1)</span><span class="sxs-lookup"><span data-stu-id="f1c74-154">Validation policies for apps and add-ins submitted to the Office Store (version 2.1)</span></span>](http://msdn.microsoft.com/library/validation-policies-for-apps-and-add-ins-submitted-to-the-office-store-version-2-1%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="f1c74-155">Начало создания надстроек Office и SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1c74-155">Start building Office and SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx)
    
 
-  [<span data-ttu-id="f1c74-156">Лицензирование надстроек Office и SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1c74-156">License your Office and SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/license-your-office-and-sharepoint-add-ins%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="f1c74-157">Развертывание и установка надстроек SharePoint: методы и параметры</span><span class="sxs-lookup"><span data-stu-id="f1c74-157">Deploying and installing SharePoint Add-ins: methods and options</span></span>](deploying-and-installing-sharepoint-add-ins-methods-and-options)
    
 
-  [<span data-ttu-id="f1c74-158">Области клиентов и области развертывания для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="f1c74-158">Tenancies and deployment scopes for SharePoint Add-ins</span></span>](tenancies-and-deployment-scopes-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="f1c74-159">Публикация надстроек SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f1c74-159">Publish SharePoint Add-ins by using Visual Studio</span></span>](publish-sharepoint-add-ins-by-using-visual-studio)
    
 
-  [<span data-ttu-id="f1c74-160">Публикация надстроек Office в Магазине</span><span class="sxs-lookup"><span data-stu-id="f1c74-160">Publishing Office Add-ins Store</span></span>](http://social.msdn.microsoft.com/Forums/en-US/officestore)
    
 

