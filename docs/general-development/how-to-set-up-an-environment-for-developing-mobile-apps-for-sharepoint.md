---
title: "Как Настройка среды разработки мобильных приложений для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: acaf556d-e20d-478d-8c59-2efd8efb9dcb
ms.openlocfilehash: ad2e9ecac7cb9129b5df24abc57b126e2cd139c8
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint"></a><span data-ttu-id="b5d60-102">Как: Настройка среды разработки мобильных приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="b5d60-102">How to: Set up an environment for developing mobile apps for SharePoint</span></span>
<span data-ttu-id="b5d60-103">Узнайте о требованиях к системе и настройке среды разработки для мобильных проектов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b5d60-103">Learn about the system requirements and configuring a development environment for SharePoint mobility projects.</span></span>
<span data-ttu-id="b5d60-104">Минимальная Настройка для работы с SharePoint мобильности проектов требуются сервере под управлением SharePoint (или SharePoint Online учетной записи) и в среде разработки на отдельной клиентской операционной системы.</span><span class="sxs-lookup"><span data-stu-id="b5d60-104">A minimal configuration for working with SharePoint mobility projects requires a server running SharePoint (or a SharePoint Online account) and a development environment on a separate client operating system.</span></span> <span data-ttu-id="b5d60-105">Установка SharePoint на клиентские операционные системы (например, Windows 7) не поддерживается, и установка средства, необходимые для разработки приложений Windows Phone, не поддерживается в операционных системах сервера (например, Windows Server 2008).</span><span class="sxs-lookup"><span data-stu-id="b5d60-105">Installing SharePoint on client operating systems (such as Windows 7) is not supported, and installing the tools necessary for Windows Phone development is not supported on server operating systems (such as Windows Server 2008).</span></span>
  
    
    


## <a name="windows-phone-development-projects-and-sharepoint-server"></a><span data-ttu-id="b5d60-106">Проектов разработки для Windows Phone и SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="b5d60-106">Windows Phone development projects and SharePoint Server</span></span>
<span data-ttu-id="b5d60-107"><a name="SP15Setupmobile_winphone"> </a></span><span class="sxs-lookup"><span data-stu-id="b5d60-107"><a name="SP15Setupmobile_winphone"> </a></span></span>

<span data-ttu-id="b5d60-108">Для создания и тестирования приложений Windows Phone, которые взаимодействуют с SharePoint, необходим доступ к серверу под управлением SharePoint или SharePoint Online учетной записи, и требуется достаточные разрешения для сайтов и списков, которые будут использоваться в ваших решений.</span><span class="sxs-lookup"><span data-stu-id="b5d60-108">To create and test Windows Phone apps that interact with SharePoint, you need access to a server running SharePoint or a SharePoint Online account, and you need sufficient permissions on the sites and lists you intend to use in your solutions.</span></span> <span data-ttu-id="b5d60-109">Мы рекомендуем использовать установки SharePoint Server, предназначенный для тестирования и разработки в качестве целевого сервера при разработке проектов.</span><span class="sxs-lookup"><span data-stu-id="b5d60-109">We recommend that you use an installation of SharePoint Server that is dedicated to testing and development as a target server while you develop your projects.</span></span> <span data-ttu-id="b5d60-110">Используйте SharePoint Server в рабочей среде как целевой сервер только после разработанных решения претерпел достаточно тестирования.</span><span class="sxs-lookup"><span data-stu-id="b5d60-110">Use SharePoint Server in a production environment as your target server only after your developed solution has undergone sufficient testing.</span></span>
  
    
    
<span data-ttu-id="b5d60-111">Подробную информацию об установке и настройке SharePoint см в разделе [Продуктов SharePoint](http://technet.microsoft.com/ru-ru/library/ee428287.aspx) в библиотеке Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="b5d60-111">For information on installing and configuring SharePoint, see the documentation in the  [SharePoint Products](http://technet.microsoft.com/ru-ru/library/ee428287.aspx) section of the Microsoft TechNet Library.</span></span> <span data-ttu-id="b5d60-112">Сведения о разработке решений с помощью SharePoint Online посетите [Центр ресурсов для разработчиков SharePoint Online](http://msdn.microsoft.com/en-us/sharepoint/gg153540.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d60-112">For information on using SharePoint Online in your development solutions, visit the [SharePoint Online Developer Resource Center](http://msdn.microsoft.com/en-us/sharepoint/gg153540.aspx).</span></span>
  
    
    
<span data-ttu-id="b5d60-113">Примеры кода в этой документации предполагается, что разработчик, работающий с примером имеет или можно получить достаточные разрешения на сайтах SharePoint, и списков, чтобы иметь возможность добавлять, изменять и удалять данные.</span><span class="sxs-lookup"><span data-stu-id="b5d60-113">For the code samples in this documentation, it is assumed that a developer working with the sample has or can obtain sufficient permissions on SharePoint sites and lists to be able to add, edit, and delete data.</span></span>
  
    
    

## <a name="configure-a-client-development-environment-for-sharepoint-mobility-projects"></a><span data-ttu-id="b5d60-114">Настройка среды разработки клиента для проектов SharePoint мобильной работы</span><span class="sxs-lookup"><span data-stu-id="b5d60-114">Configure a client development environment for SharePoint mobility projects</span></span>
<span data-ttu-id="b5d60-115"><a name="SP15Setupmobile_configure"> </a></span><span class="sxs-lookup"><span data-stu-id="b5d60-115"><a name="SP15Setupmobile_configure"> </a></span></span>

<span data-ttu-id="b5d60-116">Чтобы разработать Надстройки SharePoint для использования на устройствах Windows Phone, необходимо настроить средств разработки на компьютере под управлением клиентской операционной системы, не в операционной системе сервера.</span><span class="sxs-lookup"><span data-stu-id="b5d60-116">To develop SharePoint Add-ins for use on Windows Phone devices, you need to set up your development tools on a computer that is running a client operating system, not a server operating system.</span></span>
  
    
    

### <a name="configuring-windows-phone-sdk-80"></a><span data-ttu-id="b5d60-117">Настройка Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="b5d60-117">Configuring Windows Phone SDK 8.0</span></span>

<span data-ttu-id="b5d60-p104">Чтобы разработать Надстройки SharePoint для использования на Windows Phone 8, необходимо настроить средств разработки на компьютере, работающем под управлением версиями клиентов Windows 8 64-разрядных (x 64) или Windows 8 профессиональная. Эмулятора Windows Phone 8 требует Windows 8 Профессиональная и чтобы процессором, поддерживающим преобразования адресов второго уровня (SLAT).</span><span class="sxs-lookup"><span data-stu-id="b5d60-p104">To develop SharePoint Add-ins for use on Windows Phone 8, you need to set up your development tools on a computer that is running Windows 8 64-bit (x64) client versions or Windows 8 Pro. The Windows Phone 8 Emulator requires Windows 8 Pro, and requires a processor that supports Second Level Address Translation (SLAT).</span></span>
  
    
    

1. <span data-ttu-id="b5d60-p105">Установите на компьютере с поддерживаемой клиентской операционной системы,  [8.0 пакет SDK для Windows Phone](http://www.microsoft.com/en-us/download/details.aspx?id=35471). Windows Phone Software Development Kit (SDK) 8.0 предоставляет средства, необходимые для разработки приложений и игры для Windows Phone 8 и Windows Phone 7.5.</span><span class="sxs-lookup"><span data-stu-id="b5d60-p105">On a computer with a supported client operating system, install  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471). The Windows Phone Software Development Kit (SDK) 8.0 provides you with the tools that you need to develop apps and games for Windows Phone 8 and Windows Phone 7.5.</span></span>
    
    <span data-ttu-id="b5d60-p106">8.0 пакет SDK для Windows Phone  это среда разработки полнофункциональных для создания приложения и игры для Windows Phone 8.0 и Windows Phone 7.5. Пакет SDK для Windows Phone предоставляет изолированный Visual Studio 2012, Express edition для Windows Phone или работает в качестве надстройки для Visual Studio 2012 Professional, Premium или Ultimate выпуски. С помощью пакета SDK можно использовать имеющиеся навыки программирования и кода для создания управляемого или собственного кода приложения. Кроме того пакет SDK содержит несколько эмуляторов и дополнительные средства для профилирования и тестированию приложения Windows Phone в реальных условиях.</span><span class="sxs-lookup"><span data-stu-id="b5d60-p106">The Windows Phone SDK 8.0 is a full-featured development environment to use for building apps and games for Windows Phone 8.0 and Windows Phone 7.5. The Windows Phone SDK provides a stand-alone Visual Studio Express 2012 edition for Windows Phone or works as an add-in to Visual Studio 2012 Professional, Premium or Ultimate editions. With the SDK, you can use your existing programming skills and code to build managed or native code apps. In addition, the SDK includes multiple emulators and additional tools for profiling and testing your Windows Phone app under real-world conditions.</span></span>
    
    > <span data-ttu-id="b5d60-126">**Примечание:** Если компьютер соответствует требованиям оборудования и требования к операционной системе, но не соответствует требованиям для эмулятора Windows Phone 8, установки и выполнения 8.0 пакет SDK для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="b5d60-126">**Note:** If your computer meets the hardware and operating system requirements, but does not meet the requirements for the Windows Phone 8 Emulator, the Windows Phone SDK 8.0 will install and run.</span></span> <span data-ttu-id="b5d60-127">Тем не менее эмулятора Windows Phone 8 не будет работать, и вы не сможете для развертывания или тестирования приложения в эмуляторе Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="b5d60-127">However, the Windows Phone 8 Emulator will not function and you will not be able to deploy or test apps on the Windows Phone 8 Emulator.</span></span> <span data-ttu-id="b5d60-128">Сведения о требованиях к системе для запуска эмулятора Windows Phone видеть [программы установки и системы-требования для эмулятора Windows Phone](http://msdn.microsoft.com/ru-ru/library/ff626524).</span><span class="sxs-lookup"><span data-stu-id="b5d60-128">For information about the system requirements for running the Windows Phone Emulator, see  [Setup and System Requirements for Windows Phone Emulator](http://msdn.microsoft.com/ru-ru/library/ff626524).</span></span> 
2. <span data-ttu-id="b5d60-129">Установите  [Пакет SDK Microsoft SharePoint для Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818).</span><span class="sxs-lookup"><span data-stu-id="b5d60-129">Install  [Microsoft SharePoint SDK for Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818).</span></span>
    
    <span data-ttu-id="b5d60-130">Пакет SDK для SharePoint для Windows Phone устанавливает два шаблоны Silverlight для Windows Phone (кроме, установленных с пакет SDK для Windows Phone): шаблон приложение Windows Phone пустой SharePoint и приложения списка SharePoint для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="b5d60-130">The SharePoint SDK for Windows Phone installs two Silverlight for Windows Phone templates (in addition to those installed by the Windows Phone SDK): the Windows Phone Empty SharePoint Application template and the Windows Phone SharePoint List Application template.</span></span> <span data-ttu-id="b5d60-131">Пакет SDK также устанавливается SharePoint CSOM библиотеки, библиотеки проверки подлинности и шаблоны проектов Windows Phone и он теперь поддерживает проверку подлинности NTLM.</span><span class="sxs-lookup"><span data-stu-id="b5d60-131">The SDK also installs SharePoint CSOM libraries, an authentication library, and Windows Phone project templates, and it now supports NTLM authentication.</span></span> <span data-ttu-id="b5d60-132">Связанные интерфейсы API и шаблоны можно использовать для построения приложений Windows Phone 8 на основе SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b5d60-132">You can use the bundled APIs and templates to build Windows Phone 8 applications against SharePoint.</span></span>
    
    <span data-ttu-id="b5d60-133">Кроме того пакет SDK для SharePoint для Windows Phone устанавливает несколько вспомогательные сборки во время выполнения (в  `%ProgramFiles(x86)%\\Microsoft SDKs\\SharePoint\\v15.0\\Phone\\v8.0\\Libraries` для стандартной установки).</span><span class="sxs-lookup"><span data-stu-id="b5d60-133">Additionally, the SharePoint SDK for Windows Phone installs several supporting run-time assemblies (in  `%ProgramFiles(x86)%\\Microsoft SDKs\\SharePoint\\v15.0\\Phone\\v8.0\\Libraries` for a standard installation).</span></span>
    
  - <span data-ttu-id="b5d60-134">Microsoft.SharePoint.Client.Phone.dll</span><span class="sxs-lookup"><span data-stu-id="b5d60-134">Microsoft.SharePoint.Client.Phone.dll</span></span>
    
  
  - <span data-ttu-id="b5d60-135">Microsoft.SharePoint.Client.Phone.Runtime.dll</span><span class="sxs-lookup"><span data-stu-id="b5d60-135">Microsoft.SharePoint.Client.Phone.Runtime.dll</span></span>
    
  
  - <span data-ttu-id="b5d60-136">Microsoft.SharePoint.Client.Phone.Auth.UI</span><span class="sxs-lookup"><span data-stu-id="b5d60-136">Microsoft.SharePoint.Client.Phone.Auth.UI</span></span>
    
  
  - <span data-ttu-id="b5d60-137">Microsoft.SharePoint.Phone.Application.dll</span><span class="sxs-lookup"><span data-stu-id="b5d60-137">Microsoft.SharePoint.Phone.Application.dll</span></span>
    
  

    > <span data-ttu-id="b5d60-138">**Примечание:** Шаблоны в пакете SDK SharePoint для Windows Phone в настоящее время доступны только для проектов C#.</span><span class="sxs-lookup"><span data-stu-id="b5d60-138">**Note:** The templates in the SharePoint SDK for Windows Phone are currently available for C# projects only.</span></span> 
      > <span data-ttu-id="b5d60-139">Дополнительные сведения о шаблонах в пакете SDK SharePoint для Windows Phone можно [шаблоны приложений Overview of Windows Phone SharePoint в Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="b5d60-139">For more information about the templates in SharePoint SDK for Windows Phone, see  [Overview of Windows Phone SharePoint application templates in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span></span>
  
    
    

### <a name="configuring-windows-phone-sdk-71"></a><span data-ttu-id="b5d60-140">Настройка Windows Phone 7.1 SDK</span><span class="sxs-lookup"><span data-stu-id="b5d60-140">Configuring Windows Phone SDK 7.1</span></span>

<span data-ttu-id="b5d60-p110">Чтобы разработать Надстройки SharePoint для использования на Windows Phone 7, необходимо настроить средств разработки на компьютере, на котором работает Windows 7 (32-разрядная или 64-разрядная версия) или Пакет обновления 2 для Windows Vista (32-разрядная или 64-разрядная версия). Windows Phone Software Development Kit (SDK) 7.1 не поддерживается на Windows Server 2008 или на Windows XP.</span><span class="sxs-lookup"><span data-stu-id="b5d60-p110">To develop SharePoint Add-ins for use on Windows Phone 7, you need to set up your development tools on a computer that is running Windows 7 (32-bit or 64-bit) or Windows Vista Service Pack 2 (32-bit or 64-bit). The Windows Phone Software Development Kit (SDK) 7.1 is not supported on Windows Server 2008 or on Windows XP.</span></span>
  
    
    

1. <span data-ttu-id="b5d60-143">На компьютере с поддерживаемой клиентской операционной системы установите  [пакет SDK для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570).</span><span class="sxs-lookup"><span data-stu-id="b5d60-143">On a computer with a supported client operating system, install  [Windows Phone SDK 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570).</span></span>
    
    > <span data-ttu-id="b5d60-144">**Примечание:** Более ранней версии пакета SDK Windows Phone был с именем средств разработчика Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="b5d60-144">**Note:** An earlier version of the Windows Phone SDK was named the Windows Phone Developer Tools.</span></span> 

    <span data-ttu-id="b5d60-p111">Пакет SDK для Windows Phone устанавливает Microsoft Visual Studio 2010 Express для Windows Phone, эмулятора Windows Phone, Studio игру XNA и Blend выражений Microsoft для Windows Phone. Visual Studio 2010, экспресс-выпуск for Windows Phone  это среду разработки подходит для большинства решений для Windows Phone. Visual Studio 2010 Professional также можно использовать в качестве среды разработки предпочитаемый, но все еще необходимо установить пакет SDK для телефонов Windows, которая устанавливает необходимые надстройки Visual Studio. (Пакет SDK для Windows Phone не поддерживается в настоящее время для использования с Visual Studio 2012.)</span><span class="sxs-lookup"><span data-stu-id="b5d60-p111">The Windows Phone SDK installs Microsoft Visual Studio 2010 Express for Windows Phone, the Windows Phone Emulator, XNA Game Studio, and Microsoft Expression Blend for Windows Phone. Visual Studio 2010 Express for Windows Phone is a suitable development environment for most Windows Phone solutions. You can also use Visual Studio 2010 Professional as your preferred development environment, but you still need to install the Windows Phone SDK, which installs the necessary add-ins to Visual Studio. (The Windows Phone SDK is not currently supported for use with Visual Studio 2012.)</span></span>
    
    <span data-ttu-id="b5d60-p112">Сведения о дополнительных системных требованиях и инструкции по установке пакет SDK для Windows Phone содержатся в разделе  [Установка пакет SDK для Windows Phone](http://msdn.microsoft.com/ru-ru/library/ff402530). Сведения о требованиях к системе для запуска эмулятора Windows Phone  [программа установки, которая системы-требования для эмулятора телефона Windows](http://msdn.microsoft.com/ru-ru/library/ff626524)см.</span><span class="sxs-lookup"><span data-stu-id="b5d60-p112">For information on additional system requirements and instructions for installing the Windows Phone SDK, see  [Installing the Windows Phone SDK](http://msdn.microsoft.com/ru-ru/library/ff402530). For information about the system requirements for running the Windows Phone Emulator, see  [Setup and System Requirements for Windows Phone Emulator](http://msdn.microsoft.com/ru-ru/library/ff626524).</span></span>
    
  
2. <span data-ttu-id="b5d60-151">Установите  [Пакет SDK Microsoft SharePoint для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476).</span><span class="sxs-lookup"><span data-stu-id="b5d60-151">Install  [Microsoft SharePoint SDK for Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476).</span></span>
    
    <span data-ttu-id="b5d60-152">Пакет SDK для SharePoint для Windows Phone устанавливает два шаблоны Silverlight для Windows Phone (кроме, установленных с пакет SDK для Windows Phone): шаблон приложение Windows Phone пустой SharePoint и приложения списка SharePoint для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="b5d60-152">The SharePoint SDK for Windows Phone installs two Silverlight for Windows Phone templates (in addition to those installed by the Windows Phone SDK): the Windows Phone Empty SharePoint Application template and the Windows Phone SharePoint List Application template.</span></span>
    
    <span data-ttu-id="b5d60-153">Кроме того пакет SDK для SharePoint для Windows Phone устанавливает несколько вспомогательные сборки во время выполнения (в  `%ProgramFiles(x86)%\\Microsoft SDKs\\SharePoint\\v15.0\\Phone\\v7.1\\Libraries` для стандартной установки).</span><span class="sxs-lookup"><span data-stu-id="b5d60-153">Additionally, the SharePoint SDK for Windows Phone installs several supporting run-time assemblies (in  `%ProgramFiles(x86)%\\Microsoft SDKs\\SharePoint\\v15.0\\Phone\\v7.1\\Libraries` for a standard installation).</span></span>
    
  - <span data-ttu-id="b5d60-154">Microsoft.SharePoint.Client.Phone.dll</span><span class="sxs-lookup"><span data-stu-id="b5d60-154">Microsoft.SharePoint.Client.Phone.dll</span></span>
    
  
  - <span data-ttu-id="b5d60-155">Microsoft.SharePoint.Client.Phone.Runtime.dll</span><span class="sxs-lookup"><span data-stu-id="b5d60-155">Microsoft.SharePoint.Client.Phone.Runtime.dll</span></span>
    
  
  - <span data-ttu-id="b5d60-156">Microsoft.SharePoint.Client.Phone.Auth.UI</span><span class="sxs-lookup"><span data-stu-id="b5d60-156">Microsoft.SharePoint.Client.Phone.Auth.UI</span></span>
    
  
  - <span data-ttu-id="b5d60-157">Microsoft.SharePoint.Phone.Application.dll</span><span class="sxs-lookup"><span data-stu-id="b5d60-157">Microsoft.SharePoint.Phone.Application.dll</span></span>
    
  

    > <span data-ttu-id="b5d60-158">**Примечание:** Шаблоны в пакете SDK SharePoint для Windows Phone в настоящее время доступны только для проектов C#.</span><span class="sxs-lookup"><span data-stu-id="b5d60-158">**Note:** The templates in the SharePoint SDK for Windows Phone are currently available for C# projects only.</span></span> 
      > <span data-ttu-id="b5d60-159">Дополнительные сведения о шаблонах в пакете SDK SharePoint для Windows Phone можно [шаблоны приложений Overview of Windows Phone SharePoint в Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="b5d60-159">For more information about the templates in SharePoint SDK for Windows Phone, see  [Overview of Windows Phone SharePoint application templates in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="b5d60-160">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b5d60-160">Additional resources</span></span>
<span data-ttu-id="b5d60-161"><a name="SP15Setupmobile_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b5d60-161"><a name="SP15Setupmobile_addlresources"> </a></span></span>


-  [<span data-ttu-id="b5d60-162">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="b5d60-162">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="b5d60-163">Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="b5d60-163">Windows Phone SDK 8.0</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [<span data-ttu-id="b5d60-164">Пакет SDK Microsoft SharePoint для Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="b5d60-164">Microsoft SharePoint SDK for Windows Phone 8</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [<span data-ttu-id="b5d60-165">Пакет SDK для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="b5d60-165">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="b5d60-166">Пакет SDK Microsoft SharePoint для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="b5d60-166">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

