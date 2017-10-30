---
title: "Создание локализованных приложений для Windows Phone на основе шаблонов SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c12d7fd4-8c6b-446b-970b-1eb0e5d0a9b2
ms.openlocfilehash: 423cd5cfe84bdf23f8991a28eea70f90c83b93cf
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="build-localized-applications-for-windows-phone-based-on-the-sharepoint-templates"></a>Создание локализованных приложений для Windows Phone на основе шаблонов SharePoint
Узнайте, как построение локализуемых приложений Windows Phone, используя новые шаблоны SharePoint отличается от построение один с помощью другие шаблоны Windows Phone.
Пакет SDK для SharePoint для Windows Phone 7.1 устанавливает Windows Phone шаблонов проектов, которые можно использовать для создания приложений Windows Phone 7.1 на основе SharePoint или SharePoint 2010. Для получения дополнительных сведений см [шаблоны приложений Overview of Windows Phone SharePoint в Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md). 
  
    
    

Visual Studio использует файлы ресурсов для конкретного языка для создания сборки, которые позволяют приложению мобильных поддерживает множество языков. Дополнительные сведения об этом процессе можно  [Упаковка и развертывание ресурсов в приложениях рабочего стола](http://msdn.microsoft.com/library/b224d7c0-35f8-4e82-a705-dd76795e8d16%28Office.15%29.aspx).
> **Важные:** Если вы планируете локализации приложения для восточно-азиатских языков, обязательно ознакомьтесь с разделом «Шрифты и приложения» [Поддержка шрифта для Windows Phone](http://msdn.microsoft.com/library/b0d855ad-3fd2-4872-9a88-7f5d0a270ff9%28Office.15%29.aspx)
  
    
    


## <a name="differences-when-building-localized-applications-for-windows-phone-using-the-sharepoint-templates"></a>Отличия при создании локализованных приложений для Windows Phone с помощью шаблонов SharePoint

Построение локализуемых приложения Windows Phone, используя новые шаблоны SharePoint немного отличается от построения один с помощью другие шаблоны Windows Phone. При использовании шаблонов SharePoint немного другой формат, которого требует элемент **SupportedCultures**. Например в приложении Windows Phone standard, которая использует английский (США) для региональные параметры по умолчанию, но также поддерживает немецкий (Германия) и испанский (Испания) элемент **SupportedCultures** выглядит следующим образом:
  
    
    
 `<SupportedCultures>de-DE;es-ES;</SupportedCultures>`
  
    
    
В этом формате не работает при построении локализованного приложения Windows Phone, основанный на шаблонов SharePoint. Вместо этого найдите элемент **SupportedCultures** в файле .csproj и добавьте имена каждого языка и региональных параметров (язык), необходимые для поддержки (отличные от языка и региональных параметров по умолчанию) приложения. Разделяйте имена точкой с запятой. Должен иметь запись для каждого RESX-файл, который находится в проекте.
  
    
    
В предыдущем примере элемент **SupportedCultures** должен выглядеть следующим образом:
  
    
    
 `<SupportedCultures>de;es;</SupportedCultures>`
  
    
    
Пошаговый процесс создания локализованных приложений для Windows Phone, см  [как: создание локализованных приложений для Windows Phone](http://msdn.microsoft.com/library/9306a6ed-6efb-4f32-b850-d2e508431eeb%28Office.15%29.aspx).
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Как: создание локализованных приложений для Windows Phone](http://msdn.microsoft.com/library/9306a6ed-6efb-4f32-b850-d2e508431eeb%28Office.15%29.aspx).
    
  
-  [Глобализация и локализация для Windows Phone](http://msdn.microsoft.com/library/e82118a4-6247-4d75-a16f-749677349be4%28Office.15%29.aspx)
    
  

  
    
    

