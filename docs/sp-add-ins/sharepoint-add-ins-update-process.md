
# <a name="sharepoint-add-ins-update-process"></a><span data-ttu-id="2ec9d-101">Процесс обновления надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ec9d-101">SharePoint Add-ins update process</span></span>
<span data-ttu-id="2ec9d-102">Описание процесса обновления надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-102">Learn about the process for updating SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="2ec9d-p101">**Примечание** Название "приложения для SharePoint" меняется на "надстройки SharePoint". В процессе перехода с одного названия на другое в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="2ec9d-p102">Чтобы добавить новые возможности в надстройку SharePoint, исправить ошибку или устранить уязвимость, надстройку необходимо обновить. Обновление для надстройки развертывается с помощью пакета Надстройка SharePoint так же, как и изначальная версия надстройки. Процесс обновления надстройки SharePoint позволяет гарантировать сохранность данных, если при обновлении произойдет какой-либо сбой.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p102">You have to update a SharePoint Add-in if you add functionality, fix a bug, or make a security update. An update to an add-in is deployed in a spappsing package in the same way that the first version of the add-in is deployed. The SharePoint Add-in update process ensures that the add-in's data is preserved if the update fails for any reason.</span></span>
 

 <span data-ttu-id="2ec9d-p103">**Важно!** *Тип надстройки* невозможно изменить с помощью системы обновления. Например, нельзя заменить надстройку с размещением в SharePoint на надстройку с размещением у поставщика, используя обновление. Чтобы сделать подобное изменение, необходимо [перейти со старой надстройки на новую](#Major). В частности, так как [действие программы по ознакомлению с автоматически размещаемыми надстройками прекращено](http://blogs.office.com/2014/05/16/update-on-autohosted-apps-preview-program/), помните, что невозможно обновить надстройку с автоматическим размещением до надстройки с размещением у поставщика. Следует преобразовать надстройку, как описано в статье [Преобразование надстройки SharePoint с автоматическим размещением в надстройку с размещением у поставщика](convert-an-autohosted-sharepoint-add-in-to-a-provider-hosted-add-in).</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p103">You cannot change the add-in type using the update system. For example, you cannot change an add-in from SharePoint-hosted to provider-hosted with an update. To make a change of type, you need to migrate from an old add-in to a new one. In particular, since  the preview program for autohosted add-ins has been closed http://blogs.office.com/2014/05/16/update-on-autohosted-apps-preview-program/ , you should be aware that you cannot update an autohosted add-in to a provider-hosted add-in. You have to convert the add-in as explained in How to: Convert an autohosted SharePoint Add-in to a provider-hosted add-in.</span></span>
 


## <a name="update-process-for-a-sharepoint-add-in"></a><span data-ttu-id="2ec9d-114">Процесс обновления надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ec9d-114">Update process for a SharePoint Add-in</span></span>
<span data-ttu-id="2ec9d-115"><a name="Minor"> </a></span><span class="sxs-lookup"><span data-stu-id="2ec9d-115"></span></span>

<span data-ttu-id="2ec9d-p104">Для обновления в манифесте надстройки используется тот же код продукта, что и для исходной версии. Номер версии в манифесте надстройки должен быть больше, чем номер версии исходной надстройки или предыдущего обновления.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p104">For an update, you use the same product ID in the add-in manifest that you used for the original version. The version number in the add-in manifest should be greater than the version number of the original add-in or the most recent update.</span></span>
 

 
<span data-ttu-id="2ec9d-p105">В течение 24 часов после того как вы передадите обновление в каталог надстроек организации и в течение недели после его передачи в Магазин Office на странице **Контент сайта** каждого веб-сайта, где установлена надстройка, рядом с ее пунктом появится указание на то, что для нее доступно обновление. Чтобы обновить надстройку, пользователь может нажать ссылку, как показано на рисунке 1. Доступные обновления также отображаются в пользовательском интерфейсе управления клиента.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p105">Within 24 hours after you upload your update to an organization's add-in catalog, and within a week of uploading it to the Office Store, an indication that an update is available appears next to the add-in's listing on the **Site Contents** page of every website where it is installed. Users can click a link to update the add-in as shown in Figure 1. Available updates are also exposed in the tenant management UI.</span></span>
 

 

<span data-ttu-id="2ec9d-121">**Рисунок 1. Процесс обновления надстройки SharePoint**</span><span class="sxs-lookup"><span data-stu-id="2ec9d-121">**Figure 1 Add-in for SharePoint upgrade process**</span></span>

 

 
![Шаги по обновлению приложения в пользовательском интерфейсе](../../images/UpdatingApp_AppTileUpdateNotice.png)
 

    
 <span data-ttu-id="2ec9d-p106">**Совет** Когда вы разрабатываете обновления, можно не ждать 24 часа после каждой передачи новой версии обновления в тестовый каталог надстроек SharePoint. Сведения о том, как мгновенно обновить надстройку, см. в статье [Обновление надстройки без необходимости ожидать 24 часа](update-sharepoint-add-ins#ImmediateUpdateNotice). По умолчанию SharePoint проверяет наличие обновлений для установленных надстроек каждые 24 часа. Администратор фермы может указать другое значение для этого периода с помощью команды Командная консоль SharePoint, где n — это количество часов между проверками. `Set-SPInternalAppStateUpdateInterval -AppStateSyncHours n` Если установлено значение 0, проверка происходит при каждом выполнении задания встроенного таймера **Обновление внутреннего состояния надстройки** (по умолчанию оно выполняется каждый час). С помощью узла центра администрирования администраторы фермы могут изменить частоту выполнения задания таймера или задать его мгновенное выполнение.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p106">**Tip**   When you are developing an update, you don't want to wait 24 hours every time you upload a new version to your test SharePoint add-in catalog. See [Update an add-in without waiting 24 hours ](update-sharepoint-add-ins#ImmediateUpdateNotice) for information about how to immediately update an add-in. By default, SharePoint checks every 24 hours for updates to installed add-ins. A farm administrator can set this to another value by using the following SharePoint Management Shell command, wheren is the number of hours between checks. `Set-SPInternalAppStateUpdateInterval -AppStateSyncHours n` If the value is set to 0, then the check is made every time the built-in timer job **Internal Add-in State Update** executes, which by default is every hour. Farm administrators can use Central Admin to change the frequency of the timer job or run it immediately.</span></span>
 

<span data-ttu-id="2ec9d-p107">Когда пользователь устанавливает обновление для Надстройка SharePoint, SharePoint выполняет следующие действия. Их порядок может быть иным, и некоторые из них могут выполняться параллельно. Кроме того, в случае сбоя обновления происходит полный откат.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p107">SharePoint will do the following when a user installs an update to a SharePoint Add-in. These events do not necessarily occur in exactly this order, and some of them may occur in parallel. Also, if update fails, there is a complete rollback.</span></span>
 

 

 

- <span data-ttu-id="2ec9d-132">SharePoint выдает пользователю запрос на подтверждение изменений, запрашиваемых надстройкой.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-132">SharePoint prompts the user to approve permissions requested by the add-in.</span></span>
    
 
- <span data-ttu-id="2ec9d-133">SharePoint делает надстройку временно недоступной для пользователей.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-133">SharePoint makes the add-in unavailable to users temporarily.</span></span>
    
 
- <span data-ttu-id="2ec9d-134">Если надстройка включает пакет решения SharePoint (с расширением WSP) и содержимое этого пакета как-либо изменяется, SharePoint делает следующее:</span><span class="sxs-lookup"><span data-stu-id="2ec9d-134">If the add-in contains a SharePoint solution package (.wsp), and the contents of the solution package have changed in any way, SharePoint does the following:</span></span>
    
      - <span data-ttu-id="2ec9d-p108">создает резервную копию сайта надстройки (но в SharePoint Online, а также локальной среде SharePoint 2016 и более поздних версий резервные копии фактических данных в списках SharePoint создаются, только если при обновлении изменяется схема списка);</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p108">Makes a backup of the add-in web. (But, in SharePoint Online and in on-premises SharePoint 2016 and later, the actual data in SharePoint lists is backed up only if the update is making a change in the list's schema.)</span></span>
    
 
  - <span data-ttu-id="2ec9d-137">тестирует обновление с помощью резервной копии;</span><span class="sxs-lookup"><span data-stu-id="2ec9d-137">Tests the update of the backup.</span></span>
    
 
  - <span data-ttu-id="2ec9d-p109">если тестирование завершается успешно, обновляет исходный сайт надстройки; обратите внимание на то, что для обновления компонентов и других частей сайта надстройки используется новый WSP-файл в пакете надстройки (элементы обновления схемы компонентов были расширены в SharePoint).</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p109">If the test succeeds, updates the original add-in web. Note that the new .wsp file in the add-in package is used to update the Features and other elements in the add-in web. (The update parts of the Feature schema have been expanded in SharePoint.)</span></span>
    
 
- <span data-ttu-id="2ec9d-141">SharePoint выполняет веб-службу **UpgradedEventEndpoint**, если она зарегистрирована в манифесте надстройки.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-141">SharePoint executes the **UpgradedEventEndpoint** web service, if any is registered in the add-in manifest.</span></span>
    
     <span data-ttu-id="2ec9d-p110">**Примечание** Если надстройка размещается у поставщика, нужно реализовать логику обновления для всех ее компонентов, не относящихся к SharePoint. Чаще всего эти компоненты обновляются отдельно от обновления самой надстройки SharePoint, точно так же, как они были установлены отдельно от установки надстройки. Но может понадобиться внести определенные изменения только при обновлении пользователем надстройки SharePoint. Эту логику можно добавить в веб-службу **UpgradedEventEndpoint** или логику первого запуска после обновления в самой надстройке.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p110">**Note** If the add-in is provider-hosted, you provide the update logic for all the non-SharePoint components of the add-in. For the most part, you update these components separately from the update of the SharePoint Add-in itself, just as you installed these components separately from the installation of the add-in. But there may be some changes that should only happen when a user is updating the SharePoint Add-in. This logic can go in an **UpgradedEventEndpoint** web service or in "first run after update" logic of the add-in itself.</span></span>
- <span data-ttu-id="2ec9d-146">SharePoint восстанавливает доступ к надстройке и ее компонентам.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-146">SharePoint makes the add-in and its components available again.</span></span>
    
 

    
 <span data-ttu-id="2ec9d-p111">**Примечание** При изменении схемы любого списка на сайте надстройки создается резервная копия списка вместе с оставшимися компонентами сайта надстройки. При наличии большого количества данных в списке это может занять некоторое время. Если процесс обновления не завершается в течение 1 часа, он останавливается, а обновление откатывается.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p111">**Note** If the schema of any list in the add-in web is being changed, then the list is backed up along with the rest of the add-in web. This can take some time if there is a lot of data in the list. If the update process cannot complete in 1 hour, it stops and the update is rolled back.</span></span>
 


## <a name="migrating-from-an-old-add-in-to-a-new-one"></a><span data-ttu-id="2ec9d-150">Переход со старой надстройки на новую</span><span class="sxs-lookup"><span data-stu-id="2ec9d-150">Migrating from an old add-in to a new one</span></span>
<span data-ttu-id="2ec9d-151"><a name="Major"> </a></span><span class="sxs-lookup"><span data-stu-id="2ec9d-151"></span></span>

<span data-ttu-id="2ec9d-p112">В некоторых ситуациях может потребоваться заменить старую надстройку совершенно новой, вместо того чтобы обновлять ее. Новая надстройка может иметь то же название, что и старая, так как оно знакомо пользователям. Однако в манифесте надстройки для нее нужно задать новый код продукта, и она будет отображаться в общедоступном Магазине Office и на странице **Добавление надстройки** веб-сайтов SharePoint как отдельный элемент исходной версии.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p112">In some scenarios you may want to produce an entirely new add-in to replace an old one, rather than update the original one. The new add-in can have the same friendly name as the old, but it must be given a new product ID in the add-in manifest, and it will appear in the public Office Store and in the **Add an Add-in** page of SharePoint websites as a distinct item from the original version.</span></span>
 

 

 <span data-ttu-id="2ec9d-p113">**Примечание** Элементы в каталоге надстроек организации различаются по *имени файла* пакета надстройки, а не по идентификатору продукта или имени надстройки. Если имя файла пакета новой надстройки совпадает с именем файла пакета старой надстройки, старая надстройка будет заменена на новую в каталоге надстроек и больше не будет отображаться на странице **Добавление надстройки**. Если при передаче пакета надстройки в каталог вы включите для нее управление версиями, старая версия файла (старая надстройка) будет по-прежнему доступна в истории элемента. Вы сможете скачать старый пакет надстройки или вернуться к нему, отменив изменения, но это сделает невозможным одновременное хранение старой и новой надстроек в каталоге или на странице **Добавление надстройки** в качестве отдельных элементов.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p113">**Note** Items in an organization's add-in catalog are distinguished by the  *file name*  of the add-in package, not the product ID or the name of the add-in. If the new add-in has the same package file name as the old, it will replace the old one in the add-in catalog, and the old add-in will no longer appear on the **Add an Add-in** page. If you enable versioning on the add-in package when you upload it to the catalog, the old version of the file (which is the old app) is still available in the item's history. You can download the old add-in package or revert to it, but there is no way to have both the old and new add-ins as separate items in the catalog or on the **Add an Add-in** page, unless they have distinct file names.</span></span>
 

<span data-ttu-id="2ec9d-p114">В некоторых случаях может потребоваться перенести данные. Например, новая надстройка может использовать База данных SQL Microsoft Azure, схема которой отличается от схемы старой надстройки. Либо в новой надстройке может применяться другой механизм хранения данных, например внешняя база данных вместо списков SharePoint. В этом случае вам следует реализовать код для переноса данных.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p114">In some cases, you might need to migrate data. For example, the new add-in might use a Microsoft Azure SQL Database that has a different schema from the old add-in. Or the new add-in might use a different data storage mechanism; for example, an external database instead of SharePoint lists. You must provide the code for data migration.</span></span>
 

 
<span data-ttu-id="2ec9d-p115">Если существующие данные размещаются в месте, доступном для обработчика удаленных событий, вы можете реализовать логику переноса в веб-службе **InstalledEventEndpoint** новой надстройки. Если новая надстройка имеет доступ к существующим данным, вы также можете включить логику переноса в код, выполняемый при ее первом запуске. Если существующие данные недоступны для обработчиков удаленных событий или для новой надстройки, вы можете создать обновление для старой надстройки, чтобы добавить возможность экспорта данных и соответствующий пользовательский интерфейс. Пользователи смогут сначала обновить старую надстройку, а затем экспортировать с ее помощью данные в расположение, где они будут доступны для новой надстройки, в которой нужно обеспечить возможность импорта данных и соответствующий пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p115">If your old data is somewhere that can be accessed by a remote event handler, you can implement migration logic in an **InstalledEventEndpoint** web service of the new add-in. Alternatively, if the new add-in has access to the old data, you can put the migration logic in code that runs the first time that a user starts the new add-in. If the old data cannot be accessed by either the remote handlers or the new add-in, you can create an update of the old add-in that adds a data export capability and a UI for the capability. Users would first update the old add-in, and then use it to export the data to a location where the new add-in can access it. You include the capability and UI to import data in the new add-in.</span></span>
 

 
<span data-ttu-id="2ec9d-p116">В принципе, в новой надстройке вы можете использовать внешние источники данных, вычислительные и другие внешние компоненты, которые использовались в старой надстройке. Но учтите, что при удалении Надстройка SharePoint инфраструктура SharePoint удалит все установленные компоненты. Соответственно, рекомендуется использовать для Надстройка SharePoint только установленные им компоненты или внешние компоненты, которые не были установлены инфраструктурой SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p116">In principle, you can reuse an external data source, compute component, or other external component in the new add-in that was used in the old add-in. Consider, however, that when a SharePoint Add-in is uninstalled, the SharePoint infrastructure will uninstall everything that it installed. Accordingly, it is generally a good practice for a SharePoint Add-in to depend on only components that it installed or external components that were not installed by the SharePoint infrastructure.</span></span>
 

 

 <span data-ttu-id="2ec9d-p117">**Примечание** В случае внедрения **InstalledEventEndpoint** или **UpgradedEventEndpoint**, устанавливающей компоненты, рекомендуется также внедрить **UninstallingEventEndpoint** для удаления этих компонентов. Это соответствует принципам проектирования, требующим, чтобы надстройки были автономными и "чисто" удалялись. При этом не должны удаляться данные, которые останутся полезны пользователям и после удаления надстройки. Созданные надстройкой веб-сайты, за исключением сайта надстройки, также считаются данными.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p117">**Note** We recommend that if you implement an **InstalledEventEndpoint** or an **UpgradedEventEndpoint** that installs components, you should also implement an **UninstallingEventEndpoint** that uninstalls those same components. Doing so conforms to the design principles that add-ins should be self-contained and uninstall cleanly. However, data that would still be useful to users after the add-in is uninstalled should not be deleted. Websites created by an add-in, other than the add-in web, should usually be considered data.</span></span>
 

<span data-ttu-id="2ec9d-p118">Если и старая, и новая надстройки включают сайт надстройки, при установке новой надстройки следует создать для него новый сайт. По этой причине не следует использовать разметку XML, связанную с обновлением, в схеме компонентов SharePoint. Эта разметка не работает, поскольку существующие компоненты SharePoint не обновляются: имеющаяся надстройка заменяется новой.</span><span class="sxs-lookup"><span data-stu-id="2ec9d-p118">If the old and new add-ins each contain an add-in web, consider that a new add-in web is created when your new add-in is installed. For this reason, you should not use the update-related XML markup in the SharePoint Feature schema. Such markup does not work because you are not updating existing SharePoint components; you are replacing an old add-in with a new one.</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="2ec9d-177">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2ec9d-177">Additional resources</span></span>
<span data-ttu-id="2ec9d-178"><a name="SP15appupgrade_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2ec9d-178"></span></span>


-  [<span data-ttu-id="2ec9d-179">Обновление надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ec9d-179">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="2ec9d-180">Обновление компонентов сайта с надстройкой в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ec9d-180">Update add-in web components in SharePoint</span></span>](update-add-in-web-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="2ec9d-181">Обновление компонентов хост-сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ec9d-181">Update host web components in SharePoint</span></span>](update-host-web-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="2ec9d-182">Создание обработчика событий обновления в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ec9d-182">Create a handler for the update event in SharePoint Add-ins</span></span>](create-a-handler-for-the-update-event-in-sharepoint-add-ins)
    
 
-  <span data-ttu-id="2ec9d-183">[Обновление удаленных компонентов в надстройках SharePoint](update-remote-components-in-sharepoint-add-ins) </span><span class="sxs-lookup"><span data-stu-id="2ec9d-183">[Update remote components in SharePoint Add-ins](update-remote-components-in-sharepoint-add-ins)</span></span>
    
 
-  [<span data-ttu-id="2ec9d-184">Публикация надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ec9d-184">Publish SharePoint Add-ins</span></span>](publish-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="2ec9d-185">Важные аспекты разработки и архитектуры для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ec9d-185">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 
-  [<span data-ttu-id="2ec9d-186">Развертывание и установка надстроек SharePoint: методы и параметры</span><span class="sxs-lookup"><span data-stu-id="2ec9d-186">Deploying and installing SharePoint Add-ins: methods and options</span></span>](deploying-and-installing-sharepoint-add-ins-methods-and-options)
    
 

