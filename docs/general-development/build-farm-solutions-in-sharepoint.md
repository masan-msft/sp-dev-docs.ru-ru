---
title: "Создавайте решения фермы в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 96c32f08-ad93-49af-b8d0-9d194a48cc79
ms.openlocfilehash: 8cc5fbc9d9b26d0048cd0e42e611ff9707847079
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="build-farm-solutions-in-sharepoint"></a>Создавайте решения фермы в SharePoint
Узнайте о нашей документации по разработке, упаковки и развертывания административные расширения для SharePoint с использованием решений фермы.
## <a name="what-are-farm-solutions"></a>Что такое решений фермы
<a name="WhatAreFarmSolutions"> </a>

SharePoint имеет собственную систему для установки расширений SharePoint административным функциям, отличный от других приложений Windows и платформ. Не возникает отсутствует MSI-файл или технологии ClickOnce. Вместо этого сборки, XML и другие файлы в расширении объединены в одного файла, который вызывается пакета решения. Пакет решения имеет формат на основе .cab, но расширением WSP-файл. Пакет может содержать функций SharePoint и все их дочерние компоненты Помимо определенных типов компонентов, которые не развертываются в функции. Администраторы фермы загрузить пакеты место хранения всей ферме из которой они могут быть развернуты и их возможности.
  
    
    
В отличие от Надстройки SharePointрешения ферм содержит код, который развертывается на серверах SharePoint и выполняет вызовы объектной модели SharePoint server. Эти сборки всегда выполняются с уровнем полного доверия. Кроме того функции в решения ферм может иметь область по ширине семейства веб-сайтов, веб-приложения или всей фермы, в дополнение к области функции веб-сайта в Надстройки SharePoint. Эти аспекты решения ферм иногда сделать администраторов фермы идут на их установку, если они поступают из известного и надежного источника. По этой причине расширения SharePoint, которые в первую очередь для конечных пользователей необходимо разработать как Надстройки SharePoint, не решения ферм. Решения фермы можно использовать для настройки административных функций SharePoint, таких как задания таймера настраиваемых, настраиваемых Windows PowerShell командлетов и расширения центра администрирования. Дополнительные сведения о преимуществах Надстройки SharePoint и способов использования решения ферм см  [Сравнение надстроек SharePoint с решениями SharePoint](sharepoint-add-ins-compared-with-sharepoint-solutions.md).
  
    
    

## <a name="guide-to-the-developer-documentation-for-farm-solutions"></a>Руководство по документации для разработчиков для решений фермы
<a name="Guide"> </a>

Разработка решений фермы была изменена мало SharePoint 2010, поэтому в этом разделе содержатся ссылки на SharePoint 2010 SDK. Чтобы избежать путаницы, помнить следующее все время при использовании пакета SDK SharePoint 2010 для разработки с помощью SharePoint:
  
    
    

- Вы увидите много ссылок на «изолированных решений», в пакет SDK для SharePoint 2010. Изолированные решения с помощью пользовательского кода не поддерживаются в SharePoint. изолированные решения «без кода» еще действителен.
    
  
- Мы рекомендуем использовать этот решения ферм в первую очередь для административные расширения не были сохранены в SharePoint 2010. Таким образом многие из этих примеров и другую документацию Пакет SDK для SharePoint 2010 может быть о расширениях конечных пользователей, развернутые в виде решения ферм.
    
  
- Термины «на сервере» или «код сервера» в SharePoint 2010 SDK обратитесь к код, вызывающий серверной объектной модели SharePoint. Выполните эти термины *не* ссылаться на код, выполняющийся на удаленных веб-серверах (то есть, веб-серверы внешними по отношению к ферме SharePoint). Пример кода, вызывающего SharePoint из удаленного веб-сервера, в SharePoint 2010 и SharePoint, всегда использует один из *клиентских* объектных моделей SharePoint. В пакет SDK для SharePoint 2010 такой код будет называемое «со стороны клиента» или «код клиента».
    
  
- Сборки в решении фермы в SharePoint 2010 может быть развернуты с помощью политик безопасности пользовательского доступа (CAS). Такие политики игнорируются в SharePoint; все сборки в решениях фермы в SharePoint выполняются с уровнем полного доверия.
    
  

### <a name="packaging-and-deployment"></a>Упаковка и развертывание

Основы упаковки, установка, обновление и локализация решения ферм описаны в  [Обзор решений](http://msdn.microsoft.com/library/1983cab9-4b29-494a-a62a-0f8e83908744%28Office.15%29.aspx) и узел [Решения для фермы](http://msdn.microsoft.com/library/845f7524-b9ff-412b-aa29-3afacda91100%28Office.15%29.aspx). Разработка для определенного компонентов SharePoint для включения в решение фермы объясняется в соответствующие узлы Пакет SDK для SharePoint 2010. Большая часть компонентов в решение фермы следует инкапсулированную в настраиваемых компонентов SharePoint. Сведения о проектировании и создании функции можно узле  [Работа с компонентами](http://msdn.microsoft.com/library/ce5f5ce5-1429-439e-9261-2c4ba9788cc1%28Office.15%29.aspx)Пакет SDK для SharePoint 2010.
  
    
    

### <a name="administrative-extensions"></a>Административные расширения

Руководство по расширение административных функций в ферме SharePoint  в узле  [Администрирование Windows SharePoint Services](http://msdn.microsoft.com/library/cdcc1b8a-4144-446f-b471-03d4a754a8ab%28Office.15%29.aspx)Пакет SDK для SharePoint 2010. Там можно найти пояснения о расширении центра администрирования, создания настраиваемых Windows PowerShell командлеты, настройка обновления и миграции, настройка резервных копий и настройки ведения журнала событий SharePoint. Один раздел описывается настройка фермы SharePoint работоспособность и производительность, измерение системы. Инструкции по созданию настраиваемого задания таймера в разделе  [Практическое руководство. Запуск кода на всех веб-серверах](http://msdn.microsoft.com/library/1bbb11b4-a342-4bed-9e7a-b8b13edd0ccc%28Office.15%29.aspx).
  
    
    

## <a name="in-this-section"></a>В этом разделе
<a name="Guide"> </a>

В этом разделе описываются способы, в котором изменен разработки решений SharePoint  *имеет*  .
  
    
    

-  [Как: Настройка типа поля, с использованием обработки на стороне клиента](how-to-customize-a-field-type-using-client-side-rendering.md)
    
  
-  [URL-адреса и маркеры в SharePoint](urls-and-tokens-in-sharepoint.md)
    
  
-  [Виртуальные каталоги в решениях SharePoint](virtual-directories-in-sharepoint-solutions.md)
    
  

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15buildfarm_addlresources"> </a>


-  [Модели программирования в SharePoint](programming-models-in-sharepoint.md)
    
  
