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
# <a name="export-the-name-field-in-a-document-library-list-to-a-mobile-app"></a>Экспорт в поле имя в списке библиотеки документов в мобильных приложений

Экспорт в поле имя списка библиотеки документов в мобильных приложений с помощью мастера Visual Studio списка SharePoint. В поле имя не появляется автоматически при создании мобильного приложения для библиотеки документов в SharePoint.
В списке библиотеки документов загружаемых пользователем различных документов. Элемент списка для документа обычно содержит **заголовок**, **имя**и ссылка на документ как свойства. Если разработчик создает приложение Windows Phone 7 с библиотекой документов, в поле **имя** не экспортируется в мастере интегрированной среды разработки. Таким образом разработчик никак не просто знать имя документа. (Это так, как SharePoint не поддерживает поля типа «ФАЙЛ» по умолчанию.)
  
    
    


> **Примечание:** Свойство **Title** не включает расширение имени файла.
  
    
    


Поэтому если вы хотите извлечь документ, создания полный URL-адрес документа и откройте документ в приложении по умолчанию (например, Word), необходимо написать код для получения фактическое имя файла.
  
    
    


> **Важные:** При разработке приложения для Windows Phone 8, должны использовать Visual Studio Express 2012 г., а не в Visual Studio 2010 Express. За исключением среды разработки все сведения в этой статье применимы к созданию приложений для Windows Phone 8 и Windows Phone 7. > Для получения дополнительных сведений см [как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md). 
  
    
    


## <a name="prerequisites-for-exporting-the-name-field-of-a-document-library"></a>Необходимые условия для экспорта в поле имя библиотеки документов


- SharePoint
    
  
- Visual Studio Express 2010 с новыми шаблонами SharePoint
    
  

## <a name="customize-the-generated-classes"></a>Настройка созданных классов
<a name="HowToExportTheNameFieldInADocumentLibraryListToAMobileApp_CustomizeTheGeneratedClases"> </a>

Чтобы экспортировать **Name** поля и доступа вложения из библиотеки документов, необходимо внести несколько изменения в классе **ListDataProvider**, DisplayItemViewModel.cs и класс **DisplayForm**. Когда разработчик использует мастер создания SPList из Visual Studio, мастер создает несколько классов, следуйте шаблон разработки Model-View-ViewModel. (Для получения дополнительных сведений см [с использованием шаблона Model-View-ViewModel](http://msdn.microsoft.com/en-us/library/hh821028.aspx).) Создаются две папки: одна с именем представления, а содержит все файлы, требуемые для изменения различных представлений списка (например, DisplayForm, EditForm, списков и NewForm). Другой с именем ViewModels и содержит DisplayItemViewModel, EditItemViewModel, ListViewModel и NewItemViewModel. Будет изменен в некоторые из этих классов, созданных с помощью мастера.
  
    
    

### <a name="step-1-modify-listdataprovider-to-fetch-splistitemfile-property"></a>Шаг 1: Изменение ListDataProvider для извлечения свойств SPListItem.File


1. В классе **ListDataProvider** добавьте следующую строку кода в методе **LoadItem**.
    
     `Context.Load(spListItem, Item => Item.File);`
    
  
2. Также в классе **ListDataProvider**, добавьте следующий код в метод **LoadData**.
    
     `Context.Load(items, listItems => listItems.Include(item => item.File));`
    
  

### <a name="step-2-add-the-fileurl-and-filename-properties"></a>Шаг 2: Добавление свойства FileUrl и имя файла


- В DisplayItemViewModel.cs добавьте следующий код для **DisplayVM**.
    
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


### <a name="step-3-add-a-hyperlink-to-the-displayform-that-binds-to-fileurl-and-filename"></a>Шаг 3: Добавление гиперссылки DisplayForm, которая связывает FileUrl и имя файла


- Добавьте на форму просмотра следующие изменения.
    
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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15StoreSPlist_addlresources"> </a>


-  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Как: Создание приложения списка Windows Phone SharePoint](how-to-create-a-windows-phone-sharepoint-list-app.md)
    
  
-  [Как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [Пакет SDK для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

