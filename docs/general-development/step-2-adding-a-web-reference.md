---
title: "Этап 2. Добавление веб-ссылки"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e9175863-ddb4-4750-847d-d53cb59b33cb
ms.openlocfilehash: ced2da0e9fcbdfdca79175d0219f13dcce4e63d4
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="step-2-adding-a-web-reference"></a>Этап 2. Добавление веб-ссылки

Обнаружение веб-службы  это процесс, с помощью которого клиент определяет местоположение веб-службы и получает соответствующее описание службы. Процесс обнаружения веб-службы в Visual Studio включает опрос веб-сайта в соответствии с заданным алгоритмом. Целью этого процесса является выяснение расположения описания службы, которое является документом XML, использующим язык WSDL.
  
    
    

В описании службы указывается, какие службы доступны и каким образом осуществляется взаимодействие с этими службами. В отсутствие описания службы программное взаимодействие с веб-службой невозможно. Приложение должно располагать средствами взаимодействия с веб-службой и поиска ее расположения во время выполнения. При добавлении в проект для веб-службы веб-ссылки создается прокси-класс, который взаимодействует с веб-службой и обеспечивает локальное представление веб-службы. Дополнительные сведения см. в разделе "Веб-ссылки и создание прокси-класса веб-службы XML" в документации Microsoft Visual Studio 2005.
  
    
    


## <a name="to-add-a-web-reference"></a>Добавление веб-ссылки


1. В меню **Проект** выберите пункт **Добавить веб-ссылку**.
    
  
2. В поле **URL-адрес** диалогового окна **Добавить веб-ссылку** введите URL-адрес для получения описания веб-служб Веб-службы Excel, например `http://<server>/<customsite>/_vti_bin/excelservice.asmx` или `http://<server>/_vti_bin/excelservice.asmx`. Затем нажмите кнопку **Найти**, чтобы получить сведения о веб-службе.
    
    > **Примечание:** Можно также открыть диалоговое окно **Добавить веб-ссылку** в области **Обозреватель решений** , щелкнув правой кнопкой мыши **ссылки** и выбрав пункт **Добавить веб-ссылку**. 
3. В поле **Имя веб-ссылки** задайте имяExcelWebService.
    
  
4. Нажмите кнопку **Добавить ссылку**, чтобы добавить веб-ссылку в нужную веб-службу.
    
  
5. Visual Studio выполнит загрузку описания службы и создание прокси-класса для взаимодействия приложения и веб-служб Веб-службы Excel. 
    
  
6. Дополнительные сведения см. в разделе  [Доступ к API SOAP](accessing-the-soap-api.md).
    
  

## <a name="see-also"></a>См. также


#### <a name="concepts"></a>Основные понятия


  
    
    
 [Loop-Back SOAP Calls and Direct Linking](loop-back-soap-calls-and-direct-linking.md)
#### <a name="other-resources"></a>Другие ресурсы


  
    
    
 [Шаг 1. Создание проекта клиента веб-службы](step-1-creating-the-web-service-client-project.md)
  
    
    
 [Этап 3. Получение доступа к веб-службе](step-3-accessing-the-web-service.md)
  
    
    
 [Этап 4. Построение и тестирование приложения](step-4-building-and-testing-the-application.md)
  
    
    
 [Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel](walkthrough-developing-a-custom-application-using-excel-web-services.md)