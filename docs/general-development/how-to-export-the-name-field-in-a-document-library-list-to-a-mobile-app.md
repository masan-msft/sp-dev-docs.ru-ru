---
title: "Экспорт в поле имя в списке библиотеки документов в мобильных приложений"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 901c2012-18c6-4dbd-a787-f8650a0cc7a8
ms.openlocfilehash: 26d5da7b7e86d4517516827c907793d7b739261c
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="export-the-name-field-in-a-document-library-list-to-a-mobile-app"></a><span data-ttu-id="7de90-102">Экспорт в поле имя в списке библиотеки документов в мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="7de90-102">Export the Name field in a Document Library list to a mobile app</span></span>

<span data-ttu-id="7de90-103">Экспорт в поле имя списка библиотеки документов в мобильных приложений с помощью мастера Visual Studio списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7de90-103">Export the Name field of a Document Library list to a mobile app by using the Visual Studio SharePoint List wizard.</span></span> <span data-ttu-id="7de90-104">В поле имя не появляется автоматически при создании мобильного приложения для библиотеки документов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7de90-104">The Name field does not appear automatically when a user creates a mobile app for a document library in SharePoint.</span></span>
<span data-ttu-id="7de90-105">В списке библиотеки документов загружаемых пользователем различных документов.</span><span class="sxs-lookup"><span data-stu-id="7de90-105">In a Document Library list, a user can upload various documents.</span></span> <span data-ttu-id="7de90-106">Элемент списка для документа обычно содержит **заголовок**, **имя**и ссылка на документ как свойства.</span><span class="sxs-lookup"><span data-stu-id="7de90-106">A list item for a document typically has **Title**, **Name**, and a link to the document as properties.</span></span> <span data-ttu-id="7de90-107">Если разработчик создает приложение Windows Phone 7 с библиотекой документов, в поле **имя** не экспортируется в мастере интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="7de90-107">If a developer creates a Windows Phone 7 app against the document library, the **Name** field is not exported in the IDE wizard.</span></span> <span data-ttu-id="7de90-108">Таким образом разработчик никак не просто знать имя документа.</span><span class="sxs-lookup"><span data-stu-id="7de90-108">Thus the developer has no easy way of knowing the document name.</span></span> <span data-ttu-id="7de90-109">(Это так, как SharePoint не поддерживает поля типа «ФАЙЛ» по умолчанию.)</span><span class="sxs-lookup"><span data-stu-id="7de90-109">(This is because SharePoint does not support fields of type "FILE" by default.)</span></span>
  
    
    


> <span data-ttu-id="7de90-110">**Примечание:** Свойство **Title** не включает расширение имени файла.</span><span class="sxs-lookup"><span data-stu-id="7de90-110">**Note:** The **Title** property does not include the file name extension.</span></span>
  
    
    


<span data-ttu-id="7de90-111">Поэтому если вы хотите извлечь документ, создания полный URL-адрес документа и откройте документ в приложении по умолчанию (например, Word), необходимо написать код для получения фактическое имя файла.</span><span class="sxs-lookup"><span data-stu-id="7de90-111">So if you want to fetch a document, build the full URL of the document, and open the document in the default application (such as Word), you must write code to get the actual file name.</span></span>
  
    
    


> <span data-ttu-id="7de90-112">**Важные:** При разработке приложения для Windows Phone 8, должны использовать Visual Studio Express 2012 г., а не в Visual Studio 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="7de90-112">**Important:** If you are developing an app for Windows Phone 8, you must use Visual Studio Express 2012 instead of Visual Studio 2010 Express.</span></span> <span data-ttu-id="7de90-113">За исключением среды разработки все сведения в этой статье применимы к созданию приложений для Windows Phone 8 и Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="7de90-113">Except for the development environment, all information in this article applies to creating apps for both Windows Phone 8 and Windows Phone 7.</span></span> <span data-ttu-id="7de90-114">> Для получения дополнительных сведений см [как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="7de90-114">> For more information, see  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span></span> 
  
    
    


## <a name="prerequisites-for-exporting-the-name-field-of-a-document-library"></a><span data-ttu-id="7de90-115">Необходимые условия для экспорта в поле имя библиотеки документов</span><span class="sxs-lookup"><span data-stu-id="7de90-115">Prerequisites for exporting the Name field of a document library</span></span>


- <span data-ttu-id="7de90-116">SharePoint</span><span class="sxs-lookup"><span data-stu-id="7de90-116">SharePoint</span></span>
    
  
- <span data-ttu-id="7de90-117">Visual Studio Express 2010 с новыми шаблонами SharePoint</span><span class="sxs-lookup"><span data-stu-id="7de90-117">Visual Studio Express 2010 with the new SharePoint templates</span></span>
    
  

## <a name="customize-the-generated-classes"></a><span data-ttu-id="7de90-118">Настройка созданных классов</span><span class="sxs-lookup"><span data-stu-id="7de90-118">Customize the generated classes</span></span>
<span data-ttu-id="7de90-119"><a name="HowToExportTheNameFieldInADocumentLibraryListToAMobileApp_CustomizeTheGeneratedClases"> </a></span><span class="sxs-lookup"><span data-stu-id="7de90-119"><a name="HowToExportTheNameFieldInADocumentLibraryListToAMobileApp_CustomizeTheGeneratedClases"> </a></span></span>

<span data-ttu-id="7de90-p103">Чтобы экспортировать **Name** поля и доступа вложения из библиотеки документов, необходимо внести несколько изменения в классе **ListDataProvider**, DisplayItemViewModel.cs и класс **DisplayForm**. Когда разработчик использует мастер создания SPList из Visual Studio, мастер создает несколько классов, следуйте шаблон разработки Model-View-ViewModel. (Для получения дополнительных сведений см [с использованием шаблона Model-View-ViewModel](http://msdn.microsoft.com/en-us/library/hh821028.aspx).) Создаются две папки: одна с именем представления, а содержит все файлы, требуемые для изменения различных представлений списка (например, DisplayForm, EditForm, списков и NewForm). Другой с именем ViewModels и содержит DisplayItemViewModel, EditItemViewModel, ListViewModel и NewItemViewModel. Будет изменен в некоторые из этих классов, созданных с помощью мастера.</span><span class="sxs-lookup"><span data-stu-id="7de90-p103">To export the **Name** field and access attachments from a document library, you must make a few changes in the **ListDataProvider** class, in DisplayItemViewModel.cs, and in the **DisplayForm** class. When a developer uses the new SPList wizard from Visual Studio, the wizard creates several classes that follow the Model-View-ViewModel design pattern. (For more information, see [Using the Model-View-ViewModel Pattern](http://msdn.microsoft.com/en-us/library/hh821028.aspx).) Two folders are created: One is named Views and contains all files needed to modify various list views (such as DisplayForm, EditForm, List, and NewForm). The other is named ViewModels and contains DisplayItemViewModel, EditItemViewModel, ListViewModel, and NewItemViewModel. You will be modifying some of these classes generated by the wizard.</span></span>
  
    
    

### <a name="step-1-modify-listdataprovider-to-fetch-splistitemfile-property"></a><span data-ttu-id="7de90-125">Шаг 1: Изменение ListDataProvider для извлечения свойств SPListItem.File</span><span class="sxs-lookup"><span data-stu-id="7de90-125">Step 1: Modify ListDataProvider to fetch SPListItem.File property</span></span>


1. <span data-ttu-id="7de90-126">В классе **ListDataProvider** добавьте следующую строку кода в методе **LoadItem**.</span><span class="sxs-lookup"><span data-stu-id="7de90-126">In the **ListDataProvider** class, add the following line of code in the **LoadItem** method.</span></span>
    
     `Context.Load(spListItem, Item => Item.File);`
    
  
2. <span data-ttu-id="7de90-127">Также в классе **ListDataProvider**, добавьте следующий код в метод **LoadData**.</span><span class="sxs-lookup"><span data-stu-id="7de90-127">Also in the **ListDataProvider** class, add the following code in the **LoadData** method.</span></span>
    
     `Context.Load(items, listItems => listItems.Include(item => item.File));`
    
  

### <a name="step-2-add-the-fileurl-and-filename-properties"></a><span data-ttu-id="7de90-128">Шаг 2: Добавление свойства FileUrl и имя файла</span><span class="sxs-lookup"><span data-stu-id="7de90-128">Step 2: Add the FileUrl and FileName properties</span></span>


- <span data-ttu-id="7de90-129">В DisplayItemViewModel.cs добавьте следующий код для **DisplayVM**.</span><span class="sxs-lookup"><span data-stu-id="7de90-129">In DisplayItemViewModel.cs, add the following code to **DisplayVM**.</span></span>
    
```cs
  
public string m_fileUrl;
        public string FileUrl
        {
            get
            {
                if (string.IsNullOrEmpty(m_fileUrl))
                {
                    IListDataProvider p = this.DataProvider;
                    p.LoadItem(this.ID, (LoadItemCompletedEventArgs args) =>
                         {
                             FileUrl = this.DataProvider.SiteUrl + 
                                       args.Item.File.ServerRelativeUrl;
                         });
                }
                return m_fileUrl;
            }
            set
            {
                m_fileUrl = value;
                RaisePropertyChanged("FileUrl");
            }
        }
        public string m_fileName;
        public string FileName
        {
            get
            {
                if (string.IsNullOrEmpty(m_fileName))
                {
                    IListDataProvider p = this.DataProvider;
                    p.LoadItem(this.ID, (LoadItemCompletedEventArgs args) =>
                    {
                        FileName = args.Item.File.Name;
                    });
                }

                return m_fileName;
            }
            set
            {
                m_fileName = value;
                RaisePropertyChanged("FileName");
            }
        }
```


### <a name="step-3-add-a-hyperlink-to-the-displayform-that-binds-to-fileurl-and-filename"></a><span data-ttu-id="7de90-130">Шаг 3: Добавление гиперссылки DisplayForm, которая связывает FileUrl и имя файла</span><span class="sxs-lookup"><span data-stu-id="7de90-130">Step 3: Add a hyperlink to the DisplayForm that binds to FileUrl and FileName</span></span>


- <span data-ttu-id="7de90-131">Добавьте на форму просмотра следующие изменения.</span><span class="sxs-lookup"><span data-stu-id="7de90-131">Add the following changes to the Display form.</span></span>
    
```XML
  
<StackPanel HorizontalAlignment="Left" Orientation="Horizontal" Margin="0,5,0,5">
  <TextBlock TextWrapping="Wrap" Width="150" HorizontalAlignment="Left" 
   Style="{StaticResource PhoneTextNormalStyle}">
    FileUrl :
  </TextBlock>
  <HyperlinkButton Content="{Binding FileName}" NavigateUri="{Binding FileUrl}" 
   x:Name="hypFile" TargetName="_blank" />
</StackPanel>

```


## <a name="additional-resources"></a><span data-ttu-id="7de90-132">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7de90-132">Additional resources</span></span>
<span data-ttu-id="7de90-133"><a name="SP15StoreSPlist_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7de90-133"><a name="SP15StoreSPlist_addlresources"> </a></span></span>


-  [<span data-ttu-id="7de90-134">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="7de90-134">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="7de90-135">Как: Создание приложения списка Windows Phone SharePoint</span><span class="sxs-lookup"><span data-stu-id="7de90-135">How to: Create a Windows Phone SharePoint list app</span></span>](how-to-create-a-windows-phone-sharepoint-list-app.md)
    
  
-  [<span data-ttu-id="7de90-136">Как: Настройка среды разработки мобильных приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="7de90-136">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="7de90-137">Пакет SDK для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="7de90-137">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="7de90-138">Пакет SDK Microsoft SharePoint для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="7de90-138">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

