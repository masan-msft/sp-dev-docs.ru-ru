---
title: "Создание локализованных приложений для Windows Phone на основе шаблонов SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c12d7fd4-8c6b-446b-970b-1eb0e5d0a9b2
ms.openlocfilehash: 3c55a33469bc580d15a126585ce7ecac4babc841
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="build-localized-applications-for-windows-phone-based-on-the-sharepoint-templates"></a><span data-ttu-id="47b09-102">Создание локализованных приложений для Windows Phone на основе шаблонов SharePoint</span><span class="sxs-lookup"><span data-stu-id="47b09-102">Build localized applications for Windows Phone based on the SharePoint templates</span></span>
<span data-ttu-id="47b09-103">Узнайте, как построение локализуемых приложений Windows Phone, используя новые шаблоны SharePoint отличается от построение один с помощью другие шаблоны Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="47b09-103">Learn how building a localizable Windows Phone app using the new SharePoint templates is different from building one using other Windows Phone templates.</span></span>
<span data-ttu-id="47b09-104">Пакет SDK для SharePoint для Windows Phone 7.1 устанавливает Windows Phone шаблонов проектов, которые можно использовать для создания приложений Windows Phone 7.1 на основе SharePoint или SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="47b09-104">The SharePoint SDK for Windows Phone 7.1 installs Windows Phone project templates, which you can use to build Windows Phone 7.1 applications against SharePoint or SharePoint 2010.</span></span> <span data-ttu-id="47b09-105">Для получения дополнительных сведений см [шаблоны приложений Overview of Windows Phone SharePoint в Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="47b09-105">For more information, see  [Overview of Windows Phone SharePoint application templates in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span></span> 
  
    
    

<span data-ttu-id="47b09-p102">Visual Studio использует файлы ресурсов для конкретного языка для создания сборки, которые позволяют приложению мобильных поддерживает множество языков. Дополнительные сведения об этом процессе можно  [Упаковка и развертывание ресурсов в приложениях рабочего стола](http://msdn.microsoft.com/library/b224d7c0-35f8-4e82-a705-dd76795e8d16%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="47b09-p102">Visual Studio uses language-specific resource files to create assemblies that allow your mobile application to support many languages. For more information about this process, see  [Packaging and Deploying Resources in Desktop Apps](http://msdn.microsoft.com/library/b224d7c0-35f8-4e82-a705-dd76795e8d16%28Office.15%29.aspx).</span></span>
> <span data-ttu-id="47b09-108">**Важные:** Если вы планируете локализации приложения для восточно-азиатских языков, обязательно ознакомьтесь с разделом «Шрифты и приложения» [Поддержка шрифта для Windows Phone](http://msdn.microsoft.com/library/b0d855ad-3fd2-4872-9a88-7f5d0a270ff9%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="47b09-108">**Important:** If you plan to localize your application for East Asian languages, be sure to read the "Fonts and Your Application" section of  [Font Support for Windows Phone](http://msdn.microsoft.com/library/b0d855ad-3fd2-4872-9a88-7f5d0a270ff9%28Office.15%29.aspx)</span></span>
  
    
    


## <a name="differences-when-building-localized-applications-for-windows-phone-using-the-sharepoint-templates"></a><span data-ttu-id="47b09-109">Отличия при создании локализованных приложений для Windows Phone с помощью шаблонов SharePoint</span><span class="sxs-lookup"><span data-stu-id="47b09-109">Differences when building localized applications for Windows Phone using the SharePoint templates</span></span>

<span data-ttu-id="47b09-p103">Построение локализуемых приложения Windows Phone, используя новые шаблоны SharePoint немного отличается от построения один с помощью другие шаблоны Windows Phone. При использовании шаблонов SharePoint немного другой формат, которого требует элемент **SupportedCultures**. Например в приложении Windows Phone standard, которая использует английский (США) для региональные параметры по умолчанию, но также поддерживает немецкий (Германия) и испанский (Испания) элемент **SupportedCultures** выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="47b09-p103">Building a localizable Windows Phone app using the new SharePoint templates is slightly different from building one using other Windows Phone templates. When you use the SharePoint templates, the **SupportedCultures** element requires a slightly different format. For example, in a standard Windows Phone app that uses English (United States) for its default culture but also supports German (Germany) and Spanish (Spain), the **SupportedCultures** element appears as follows:</span></span>
  
    
    
 `<SupportedCultures>de-DE;es-ES;</SupportedCultures>`
  
    
    
<span data-ttu-id="47b09-p104">В этом формате не работает при построении локализованного приложения Windows Phone, основанный на шаблонов SharePoint. Вместо этого найдите элемент **SupportedCultures** в файле .csproj и добавьте имена каждого языка и региональных параметров (язык), необходимые для поддержки (отличные от языка и региональных параметров по умолчанию) приложения. Разделяйте имена точкой с запятой. Должен иметь запись для каждого RESX-файл, который находится в проекте.</span><span class="sxs-lookup"><span data-stu-id="47b09-p104">This format does not work when you build a localized Windows Phone app that is based on the SharePoint templates. Instead, locate the **SupportedCultures** element in the .csproj file and add the names of each culture (language) that your application needs to support (other than the default culture). Separate the names using semicolons. You should have an entry for each .resx file that is in the project.</span></span>
  
    
    
<span data-ttu-id="47b09-117">В предыдущем примере элемент **SupportedCultures** должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="47b09-117">For the previous example, the **SupportedCultures** element should appear as follows:</span></span>
  
    
    
 `<SupportedCultures>de;es;</SupportedCultures>`
  
    
    
<span data-ttu-id="47b09-118">Пошаговый процесс создания локализованных приложений для Windows Phone, см  [как: создание локализованных приложений для Windows Phone](http://msdn.microsoft.com/library/9306a6ed-6efb-4f32-b850-d2e508431eeb%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="47b09-118">To see a step-by-step process of how to build a localized application for Windows Phone, see  [How to: Build a Localized Application for Windows Phone](http://msdn.microsoft.com/library/9306a6ed-6efb-4f32-b850-d2e508431eeb%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="47b09-119">См. также</span><span class="sxs-lookup"><span data-stu-id="47b09-119">See also</span></span>
<span data-ttu-id="47b09-120"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="47b09-120"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="47b09-121">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="47b09-121">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  <span data-ttu-id="47b09-122">[Как: создание локализованных приложений для Windows Phone](http://msdn.microsoft.com/library/9306a6ed-6efb-4f32-b850-d2e508431eeb%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="47b09-122">[How to: Build a Localized Application for Windows Phone](http://msdn.microsoft.com/library/9306a6ed-6efb-4f32-b850-d2e508431eeb%28Office.15%29.aspx).</span></span>
    
  
-  [<span data-ttu-id="47b09-123">Глобализация и локализация для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="47b09-123">Globalization and Localization for Windows Phone</span></span>](http://msdn.microsoft.com/library/e82118a4-6247-4d75-a16f-749677349be4%28Office.15%29.aspx)
    
  

  
    
    

