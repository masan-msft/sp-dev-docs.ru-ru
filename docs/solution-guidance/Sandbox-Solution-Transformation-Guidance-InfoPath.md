---
title: "Изолированная преобразования руководство по решениям для-InfoPath"
ms.date: 11/03/2017
ms.openlocfilehash: 62a6d4015cbfba99468d47ac11aa1a8cd8271fb0
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="sandbox-solution-transformation-guidance---infopath"></a>Изолированная преобразования руководство по решениям для-InfoPath
При использовании форм InfoPath с кодом, а затем зависят от этих форм InfoPath на основе кода изолированных решений для выполнения кода. Эта статья поможет вам устранить или преобразования формы InfoPath, чтобы больше не зависимости решения не изолированной среды.

_**Применимо к:** Формы InfoPath для SharePoint Online | SharePoint 2013 | SharePoint 2016_

SharePoint online и изолированной среды на основе кода решения, [рекомендуется использовать](https://blogs.msdn.microsoft.com/sharepointdev/2014/01/14/deprecation-of-custom-code-in-sandboxed-solutions/) обратно в 2014 г запущен процесс, чтобы полностью удалить эту возможность. На основе кода изолированных решений также являются устаревшими в SharePoint 2013 и в SharePoint 2016.

## <a name="analyze-and-if-possible-fix-your-infopath-forms"></a>Анализ и по возможности исправить формы InfoPath
<a name="sectionSection1"> </a>

В этом разделе мы покажем анализ и устранение модель, можно применить к формы InfoPath. В зависимости от формы можно просто **исправить** формы и снова развернуть ее или при необходимости **переместить вне InfoPath** и использовать альтернативный подход в полной мере реализовать необходимые функциональные возможности. Однако перед выполнением этих действий **необходимо Оценка потребности бизнеса в форме**: мы часто увидеть часто старых форм, которые не являются бизнес-соответствующих больше и в этих случаях проще просто удалить форму. 

### <a name="how-do-i-know-that-ive-infopath-forms-with-code-behind"></a>Как узнать, что у меня есть форм InfoPath с выделенным кодом
Рекомендуется, для использования **[средства сканера изолированные решения SharePoint](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.SandBoxTool)** в качестве отчета из этой программы появится сообщение о том Если изолированные решения поступает из файла InfoPath. Кроме того средство также сообщит вам, если используемые сборки в решении «бесполезная», как описано далее в этой статье.

### <a name="are-my-forms-still-relevant"></a>Относятся Мои формы по-прежнему?
Перед освоение рабочих исправлению или преобразования важно вопрос: важна эту форму по-прежнему для бизнес. Если та, перейдите к следующей главе, если не вы должны помнить о данных, созданных с помощью этой формы. Обычно данных был создан как InfoPath XML-файлы которого live в списке SharePoint. При удалении формы вы не сможете больше визуализировать данные: в некоторых случаях это нормально, поскольку формы и данные не учитываются больше, но в случае, если требуется разрешить доступ к данным можно преобразовать InfoPath XML-файлы данных списка (элементы) SharePoint. [Репозиторий PnP модернизации содержит пример, в котором показано, как это можно сделать](https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath/Migration/EmpRegConsole "образец, показывающих, как для преобразования из InfoPath из XML в данные списка").

### <a name="downloading-the-infopath-form-xsn-file-for-inspection"></a>Загрузка форм InfoPath (XSN-файл) для проверки
В шаге раздела, подтверждения, что у вас есть форм InfoPath, которые требуют работы в этом разделе вы научитесь загрузить эти формы. Формы InfoPath с кодом программной части, либо развернуты как «Библиотека форм» или «Тип содержимого узла». В зависимости от выбранного модель публикации вы можете загрузить форм следующим образом.

#### <a name="download-form-library-deployed-infopath-forms"></a>Файл для загрузки «библиотека форм» развертывание форм InfoPath
В этом случае файла XSN находится внутри папки форм библиотеки форм, в который был развернут форм InfoPath. Знакомство с библиотекой форм может занять внимание на имя пакета WSP как если бы образом это соглашение о: «InfoPath Form_**LibName**_id». Поэтому при наличии библиотеки необходимо загрузить файл template.xsn из папки форм библиотеки. Это можно сделать, создав url-адресу следующего вида: **URL-адрес библиотеки + «Forms/template.xsn»** , как показано в этом примере `https://contoso.sharepoint.com/sites/infopath1/IHaveCodeBehind/Forms/template.xsn` и использование браузера для загрузки файла.

#### <a name="download-site-content-type-deployed-infopath-forms"></a>Файл для загрузки «тип содержимого узла» развертывание форм InfoPath
Формы InfoPath, развернутые в виде типа контента имеют их XSN файлов, хранящихся в библиотеке форм, который был подключен к типу контента, как время развертывания формы. Как и в предыдущем разделе может получить имя библиотеки из WSP имя пакета. Каковы отличия, настоящее время —, что форма хранится в виде файла в библиотеке обнаруженного так просто можно загрузить из библиотеки форм. 

### <a name="fixing-your-infopath-forms"></a>Исправление форм InfoPath
Предыдущих разделах показано записи с учетом форм InfoPath с выделенным кодом, но они действительно содержат полезные кода? Что мы указано, что существует много форм, для которых автор формы случайно нажатии на кнопке **Редактор кода** в ленте **для разработчиков** InfoPath:

![Фоновый код InfoPath](media/Sandbox-Solution-Transformation-Guidance-InfoPath/InfoPathCodeBehind.png)

После этого вам придется фоновый код..., но этот код за не делает ничего и путем удаления можно преобразовать форму InfoPath с кодом программной части регулярного форму InfoPath, которая не имеет кода фонового и таким образом не зависимости на изолированные решения!

#### <a name="how-do-i-know-the-code-behind-is-useless"></a>Как узнать, что с выделенным кодом «бесполезная»?
[Изолированные решения SharePoint сканера](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.SandBoxTool) сообщит вам, если InfoPath имеет смысла кода, но если вы хотите Дополнительные сведения и продолжите чтение. Могут возникнуть как для различения фоновый код бесполезная и необходимые как может устранять только первой категории. При наличии исходного развернутое формы (поэтому не по одному, загруженный в предыдущих действиях) по-прежнему можно создать взглянуть на код. Ниже показан пустой кода по умолчанию, и те, кто следующего кода нажмите эту форму можно устранить, удалив код:

```C#
using Microsoft.Office.InfoPath;
using System;
using System.Xml;
using System.Xml.XPath;

namespace Form1
{
    public partial class FormCode
    {
        // Member variables are not supported in browser-enabled forms.
        // Instead, write and read these values from the FormState
        // dictionary using code such as the following:
        //
        // private object _memberVariable
        // {
        //     get
        //     {
        //         return FormState["_memberVariable"];
        //     }
        //     set
        //     {
        //         FormState["_memberVariable"] = value;
        //     }
        // }

        // NOTE: The following procedure is required by Microsoft InfoPath.
        // It can be modified using Microsoft InfoPath.
        public void InternalStartup()
        {
        }
    }
}
```

В случае, если имеется только файл XSN, который загружена во время предыдущего действия, которые можно переименовать файл XSN CAB-файлу (например template.cab), извлечение сборки и с помощью средств отражения .net (как и открытым кодом [ILSpy](http://ilspy.net/ "ILSpy .NET открытым исходным кодом браузер сборки и декомпилятор")) для проверки кода. Стандартные представления бесполезная фоновый код выглядит следующим образом в ILSpy:

![Бесполезная кода по результатам ILSpy](media/Sandbox-Solution-Transformation-Guidance-InfoPath/ilspyoutput.png)

#### <a name="dropping-code-behind-from-infopath-forms-to-fix-them"></a>Удаление фоновый код из формы InfoPath их устранения
Если подтверждает, что ваш код не имеет смысла можно легко поместите его:
- Открытие формы в **InfoPath designer** (щелкните правой кнопкой мыши-структуры)
- Перейдите на **Параметры формы** с помощью файла - Info
- Выберите категорию **по программированию** и выберите команду **Удалить код**
- **Публикация формы еще раз** с помощью файла - Info - Быстрая публикация
- **Отключение связанных изолированные решения** с помощью параметров веб - решений
- **Подтверждение** формы работает, как ожидалось
- **Удаление** изолированного решения

Если у вас нет доступа к InfoPath XSN файла и исходный код больше **по-прежнему можно устранить эти формы посредством просто отключения изолированные решения, которые имеют только код «бесполезная»**. Делать это только для из них, упомянутые в выходные данные отчета решения изолированной среды с IsEmptyInfoPathAssembly = true.

## <a name="migrate-your-infopath-forms"></a>Перенос форм InfoPath
<a name="sectionSection2"></a> Инструкции в предыдущей главе не применима для формы InfoPath его по сути означает, что форма будет по-прежнему business соответствующих и содержит код, который нельзя удалить. Если это так типичное решение удаляется от InfoPath, который может выполняться разными способами:
- Создание приложения с помощью [Azure PowerApps](https://powerapps.microsoft.com/en-us/ "Azure PowerApps") или [Microsoft поток](https://flow.microsoft.com/en-us/search/?q=sharepoint "Поток Microsoft") 

![Microsoft потока и Azure PowerApps](media/Sandbox-Solution-Transformation-Guidance-InfoPath/powerappsflow.png)

- Создание надстройки SharePoint, которая использует удаленного интерфейса API для чтения и записи данных SharePoint

### <a name="building-sharepoint-add-ins-to-replace-your-infopath-forms"></a>Создание надстройки SharePoint's замена форм InfoPath
Если вы решили использовать регулярное SharePoint надстройки для замены формы InfoPath имеется несколько вариантов. Ниже приведены три варианта, которые мы работали в работе более подробно, но как указанного вполне варианты можно использовать эти. Три варианта, которые мы хотели углубленно являются:
- [На knockout.js основе одной страницы приложения (SPA)] (https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath/Samples/EmployeeRegistration.KnockOut.SinglePageApp "Пример SPA, использующий knockout.js")

![Пример выход](media/Sandbox-Solution-Transformation-Guidance-InfoPath/knockoutsample.png)

- [ASP.Net MVC SharePoint надстройке] (https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath/Samples/EmployeeRegistration.MVC "Добавить в SharePoint с помощью ASP.Net MVC")
- [Надстройка SharePoint форм ASP.Net] (https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath/Samples/EmployeeRegistration.Forms "Добавить в SharePoint с помощью форм ASP.Net")

Для улучшения вы с преобразование InfoPath форм **мы приведены 11 Общие шаблоны для программирования InfoPath и показано, как реализовать эти шаблоны, с использованием выше 3 упомянутый SharePoint параметры надстройки**. Для этого сначала разработанный [ссылку формы InfoPath](https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath/Reference/EmployeeRegistration "формы InfoPath ссылку") использует наиболее распространенные InfoPath, шаблоны кода и затем перенесены данной форме в версии 3 добавить в SharePoint. Следующие ссылки покажите этих общих шаблонов:
- [Заполнение полей при загрузке формы - набор сведений о пользователе] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Populating%20fields%20on%20form%20load-set%20user%20information.md "Заполнение полей при загрузке формы - набор сведений о пользователе")
- [Заполнение полей при загрузке формы — чтение сведения о списке] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Populating%20fields%20on%20form%20load-read%20list%20information.md "Заполнение полей при загрузке формы — чтение сведения о списке")
- [Заполнение полей при загрузке формы — чтение данных списка] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Populating%20fields%20on%20form%20load-read%20list%20data.md "Заполнение полей при загрузке формы — чтение данных списка")
- [Отправка формы с помощью кода] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Submit%20the%20form%20via%20code.md "Отправка формы с помощью кода")
- [Переключение представления после отправки формы] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Switching%20view%20after%20form%20submission.md "Переключение представления после отправки формы")
- [Извлечение пользовательских данных] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Retrieving%20user%20data.md "Извлечение пользовательских данных")
- [Прочитайте сбора данных и настройка нескольких элементов управления] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Read%20data%20collection%20and%20set%20multiple%20controls.md "Прочитайте сбора данных и настройка нескольких элементов управления")
- [Загрузить каскадные таблицы данных] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Cascading%20data%20load.md "Загрузить каскадные таблицы данных")
- [Передача или удалить вложения.] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Upload%20or%20Delete%20Attachments.md "Передача или удалить вложения.")
- [Добавить или удалить пользователя из группы сайтов] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Add%20or%20remove%20user%20from%20site%20groups.md "Добавить или удалить пользователя из группы сайтов")
- [Загрузка существующего элемента в форме] (https://github.com/SharePoint/PnP-Transformation/blob/master/InfoPath/Guidance/Patterns/Load%20existing%20item%20in%20form.md "Загрузка существующего элемента в форме")


### <a name="migrating-your-infopath-data"></a>Перенос данных InfoPath
После перемещения формы InfoPath для нового решения может потребоваться перенос данных из InfoPath XML для регулярного данных списка SharePoint или на уровне данных почтой. Поскольку файлы InfoPath, XML-файлов довольно прост в чтение и тех, преобразование. [Репозиторий PnP модернизации содержит пример, в котором показано, как это можно сделать](https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath/Migration/EmpRegConsole "образец, показывающих, как для преобразования из InfoPath из XML в данные списка").

### <a name="code-based-operations-are-disabled-and-now-my-existing-forms-dont-open-anymore"></a>Операции с на основе кода и теперь Мои существующей формы не закрыт
Сразу же операции с кодом на основе это означает, что код не может больше выполняются в изолированной среде. Если вы добавили форм, в которых выполнения кода это также означает, что не будет больше работать открытия существующих форм. Шаги, описанные ниже поможет вам обрабатывать это:
 - Если перенесены формы InfoPath в новое решение затем вероятнее всего уже преобразования данных и таким образом вы готовы
 -  Если подписано сохранить форму как (например, поскольку она не бизнес-больше критические), но по-прежнему требуется открытия существующих форм, затем можно выполнить одно из следующих действий:
    - Удалите с выделенным кодом из формы и повторной публикации (обратитесь к разделу **Удаление фоновый код из формы InfoPath, чтобы исправить их** )
    - Используйте для открытия формы InfoPath клиента
    - Выполнение миграции данных формы в простых данных списка SharePoint (обратитесь к разделу **переносе данных InfoPath** )

