---
title: "Реактивные и нереактивные веб-части SharePoint"
ms.date: 9/25/2017
ms.openlocfilehash: 33f46f3582555690ba5e9f7e08e7a0bce8c5b505
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="reactive-and-nonreactive-sharepoint-web-parts"></a><span data-ttu-id="37813-102">Реактивные и нереактивные веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="37813-102">Reactive and nonreactive SharePoint web parts</span></span>

<span data-ttu-id="37813-103">Реактивные веб-части работают только на стороне клиента. Нереактивные веб-части содержат элементы, для работы которых необходим сервер.</span><span class="sxs-lookup"><span data-stu-id="37813-103">Reactive web parts are client-side only; nonreactive web parts have elements that require a server to operate.</span></span> <span data-ttu-id="37813-104">Рекомендуем создавать реактивные веб-части SharePoint, так как они больше соответствуют модели пользовательского интерфейса и принципам WYSIWYG для разработки.</span><span class="sxs-lookup"><span data-stu-id="37813-104">We recommend that you build your SharePoint web parts to be reactive, because that best fits the UX model and WYSIWYG principles for authoring.</span></span> <span data-ttu-id="37813-105">Однако в некоторых случаях создавать реактивные веб-части может быть невозможно или невыгодно.</span><span class="sxs-lookup"><span data-stu-id="37813-105">However, it might not be possible or cost-effective in all cases to build reactive web parts.</span></span>


## <a name="reactive-web-parts"></a><span data-ttu-id="37813-106">Реактивные веб-части</span><span class="sxs-lookup"><span data-stu-id="37813-106">Reactive vs non-reactive web parts</span></span>

<span data-ttu-id="37813-107">Реактивные веб-части полностью размещаются на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="37813-107">Reactive web parts are fully client-side web parts.</span></span> <span data-ttu-id="37813-108">Это означает, что каждый компонент, настроенный в области свойств, будет отражать изменения, внесенные в веб-части на странице.</span><span class="sxs-lookup"><span data-stu-id="37813-108">This means that each component configured in the property pane will reflect the change made within the web part on the page.</span></span> <span data-ttu-id="37813-109">Например, в веб-части "Список дел" при снятии флажка "Выполненные задачи" скрывается соответствующее представление в веб-части.</span><span class="sxs-lookup"><span data-stu-id="37813-109">For example, for the To-Do List web part, unchecking “Completed Tasks” will hide this view in the web part.</span></span>

![Реактивная веб-часть](../images/design-reactive-01.png)


## <a name="nonreactive-web-parts"></a><span data-ttu-id="37813-111">Нереактивные веб-части</span><span class="sxs-lookup"><span data-stu-id="37813-111">Nonreactive web parts</span></span>
<span data-ttu-id="37813-112">Нереактивные веб-части работают не только на стороне клиента. Как правило, одному или нескольким свойствам требуется совершить вызов, чтобы задать, получить или сохранить данные на сервере.</span><span class="sxs-lookup"><span data-stu-id="37813-112">Non-reactive web parts are not fully client side and generally one or more properties need to make a call to set/pull or store data on a server. In this case, you should enable the Apply and Cancel buttons at the bottom of the properties pane.</span></span> <span data-ttu-id="37813-113">Для нереактивных веб-частей следует включить кнопку **Применить** в нижней части области свойств.</span><span class="sxs-lookup"><span data-stu-id="37813-113">For nonreactive web parts, you should enable the **Apply** button at the bottom of the property pane.</span></span>

<span data-ttu-id="37813-114">Вы также можете назначить кнопке **Применить** более конкретное действие.</span><span class="sxs-lookup"><span data-stu-id="37813-114">You can also customize the **Apply** button to be a more specific action.</span></span> <!-- Is this a reference to an image? (design-wp-pp-non-reactive.png) -->

![Нереактивная веб-часть с кнопками "Применить" и "Отменить"](../images/design-reactive-02.png)


<span data-ttu-id="37813-116">В приведенных ниже примерах показаны нереактивные веб-части в контексте [трех структур областей свойств](design-a-web-part.md).</span><span class="sxs-lookup"><span data-stu-id="37813-116">The following examples show nonreactive web parts in the context of the [three property pane structures](design-a-web-part.md).</span></span>

<span data-ttu-id="37813-117">**Пример одиночной области**</span><span class="sxs-lookup"><span data-stu-id="37813-117">**Single pane example**</span></span>

![Нереактивная веб-часть с одиночной областью свойств](../images/design-reactive-03.png)

<span data-ttu-id="37813-119">**Пример групп области-гармошки**</span><span class="sxs-lookup"><span data-stu-id="37813-119">**Accordion groups example**</span></span>

![Нереактивная веб-часть с областью свойств в виде гармошки](../images/design-reactive-04.png)

<span data-ttu-id="37813-121">**Пример ступенчатой области**</span><span class="sxs-lookup"><span data-stu-id="37813-121">**Steps pane example**</span></span>

![Нереактивная веб-часть со ступенчатой областью свойств](../images/design-reactive-05.png)