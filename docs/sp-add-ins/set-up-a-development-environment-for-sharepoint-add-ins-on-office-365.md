---
title: Настройка среды разработки надстроек SharePoint в Office 365
description: Установите Visual Studio и получите подписку разработчика Office 365.
ms.date: 03/14/2018
ms.prod: sharepoint
ms.openlocfilehash: 47fa3a86561f77094029995569d0b8f62a89bf89
ms.sourcegitcommit: ad9b18a3fc81d9561383413644120e7255d31d61
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2018
---
# <a name="set-up-a-development-environment-for-sharepoint-add-ins-on-office-365"></a>Настройка среды разработки надстроек SharePoint в Office 365

Чтобы получить представление о доступных вариантах, прежде чем выполнять описанные в этой статье действия, см. статью [Средства и среды для разработки надстроек SharePoint](tools-and-environments-for-developing-sharepoint-add-ins.md). 

Если вы не уверены, какие надстройки SharePoint требуется создавать, см. статью [Надстройки SharePoint](sharepoint-add-ins.md).
 
<a name="devenv_vs"> </a>

## <a name="install-visual-studio-and-tools-on-your-computer"></a>Установка Visual Studio и инструментов на компьютере

- Если вы еще не установили **Visual Studio** 2013 или более поздней версии, сделайте это, следуя инструкциям из статьи [Установка Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio). Рекомендуем использовать [последнюю версию из Центра загрузки Майкрософт](https://www.visualstudio.com/downloads/download-visual-studio-vs).
 
- Visual Studio включает **Инструменты разработчика Microsoft Office для Visual Studio**. Иногда выпуск новой версии этих инструментов не совпадает с выходом обновлений Visual Studio. Чтобы убедиться, что у вас установлена последняя версия этих инструментов, запустите [установщик набора "Инструменты разработчика Office для Visual Studio 2013"](http://aka.ms/OfficeDevToolsForVS2013) или [установщик набора "Инструменты разработчика Office для Visual Studio 2015"](http://aka.ms/OfficeDevToolsForVS2015). 

Сверяйтесь с [более ранними версиями Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx) или другой [документацией по Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/). 

### <a name="verbose-logging-in-visual-studio"></a>Подробное ведение журнала в Visual Studio

Выполните указанные ниже действия, чтобы включить подробное ведение журнала.

1. Откройте реестр и перейдите к разделу **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\ _nn.n_\SharePointTools**, где _nn.n_ — это номер версии Visual Studio, например 12.0 или 14.0.

2. Добавьте ключ DWORD под названием **EnableDiagnostics**.

3. Присвойте ключу значение **1**.

Путь реестра в будущих версиях Visual Studio изменится.


<a name="o365_signup"> </a>

## <a name="sign-up-for-an-office-365-developer-subscription"></a>Получение подписки разработчика Office 365

> [!NOTE]
> Возможно, у вас уже есть доступ к подписке разработчика Office 365: 
> - **У вас есть подписка на Visual Studio (MSDN)?** Подписчики Visual Studio Ultimate и Visual Studio Premium с MSDN получают подписку разработчика Office 365 бесплатно. [Воспользуйтесь этим преимуществом сегодня](https://msdn.microsoft.com/subscriptions/manage/default.aspx). 
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
 

## <a name="see-also"></a>См. также
<a name="SP15SetupSPO365_bk_addlresources"> </a>

- [Надстройки SharePoint](sharepoint-add-ins.md)
- [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md)
- [Знакомство с созданием надстроек SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md) 

    
 
