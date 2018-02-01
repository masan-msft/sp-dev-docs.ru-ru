---
title: "Реактивные и нереактивные веб-части SharePoint"
description: "Реактивные веб-части выполняются полностью на стороне клиента. Нереактивные веб-части содержат элементы, для работы которых требуется сервер."
ms.date: 01/23/2018
ms.openlocfilehash: 74d1ccfd1ed882d5efbdd8181ac44ceb1a1674eb
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="reactive-and-nonreactive-sharepoint-web-parts"></a><span data-ttu-id="4ee0c-103">Реактивные и нереактивные веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ee0c-103">Reactive and nonreactive SharePoint web parts</span></span>

<span data-ttu-id="4ee0c-104">Реактивные веб-части работают только на стороне клиента. Нереактивные веб-части содержат элементы, для работы которых необходим сервер.</span><span class="sxs-lookup"><span data-stu-id="4ee0c-104">Reactive web parts are client-side only; nonreactive web parts have elements that require a server to operate.</span></span> <span data-ttu-id="4ee0c-105">Рекомендуем создавать реактивные веб-части SharePoint, так как они больше соответствуют модели пользовательского интерфейса и принципам WYSIWYG для разработки.</span><span class="sxs-lookup"><span data-stu-id="4ee0c-105">We recommend that you build your SharePoint web parts to be reactive, because that best fits the UX model and WYSIWYG principles for authoring.</span></span> <span data-ttu-id="4ee0c-106">Однако в некоторых случаях создавать реактивные веб-части может быть невозможно или невыгодно.</span><span class="sxs-lookup"><span data-stu-id="4ee0c-106">However, it might not be possible or cost-effective in all cases to build reactive web parts.</span></span>


## <a name="reactive-web-parts"></a><span data-ttu-id="4ee0c-107">Реактивные веб-части</span><span class="sxs-lookup"><span data-stu-id="4ee0c-107">Reactive web parts</span></span>

<span data-ttu-id="4ee0c-108">Реактивные веб-части выполняются полностью на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="4ee0c-108">Reactive web parts are fully client-side web parts.</span></span> <span data-ttu-id="4ee0c-109">Это означает, что каждый компонент, настроенный в области свойств, отражает изменения, внесенные в веб-части на странице.</span><span class="sxs-lookup"><span data-stu-id="4ee0c-109">This means that each component configured in the property pane will reflect the change made within the web part on the page.</span></span> <span data-ttu-id="4ee0c-110">Например, снятие флажка "Выполненные задачи" скрывает это представление в веб-части "Список дел".</span><span class="sxs-lookup"><span data-stu-id="4ee0c-110">For example, for the To-Do List web part, unchecking “Completed Tasks” will hide this view in the web part.</span></span>

<img alt="A reactive web part" src="../images/design-reactive-01.png" width="850">

## <a name="nonreactive-web-parts"></a><span data-ttu-id="4ee0c-111">Нереактивные веб-части</span><span class="sxs-lookup"><span data-stu-id="4ee0c-111">Nonreactive web parts</span></span>
<span data-ttu-id="4ee0c-112">Нереактивные веб-части работают не только на стороне клиента. Как правило, одному или нескольким свойствам требуется выполнить вызов, чтобы задать, получить или сохранить данные на сервере.</span><span class="sxs-lookup"><span data-stu-id="4ee0c-112">Nonreactive web parts are not fully client-side; generally, one or more properties need to make a call to set/pull or store data on a server.</span></span> <span data-ttu-id="4ee0c-113">Для нереактивных веб-частей следует включить кнопку **Применить** в нижней части области свойств.</span><span class="sxs-lookup"><span data-stu-id="4ee0c-113">For nonreactive web parts, you should enable the **Apply** button at the bottom of the property pane.</span></span>

<span data-ttu-id="4ee0c-114">Вы также можете назначить кнопке **Применить** более конкретное действие.</span><span class="sxs-lookup"><span data-stu-id="4ee0c-114">You can also customize the **Apply** button to be a more specific action.</span></span> <!-- Is this a reference to an image? (design-wp-pp-non-reactive.png) -->

<img alt="A nonreactive web part with Apply and Cancel buttons" src="../images/design-reactive-02.png" width="850">

<br/>

<span data-ttu-id="4ee0c-115">В приведенных ниже примерах показаны нереактивные веб-части в контексте [трех разных областей свойств](design-a-web-part.md).</span><span class="sxs-lookup"><span data-stu-id="4ee0c-115">The following examples show nonreactive web parts in the context of the [three property pane structures](design-a-web-part.md).</span></span>

<span data-ttu-id="4ee0c-116">**Пример одиночной области**</span><span class="sxs-lookup"><span data-stu-id="4ee0c-116">**Single pane example**</span></span>

<img alt="A nonreactive web part with a single pane property structure" src="../images/design-reactive-03.png" width="850">

<br/>

<span data-ttu-id="4ee0c-117">**Пример групп элементов "аккордеон"**</span><span class="sxs-lookup"><span data-stu-id="4ee0c-117">**Accordion groups example**</span></span>

<img alt="A nonreactive web part with an according groups pane property structure" src="../images/design-reactive-04.png" width="850">

<br/>

<span data-ttu-id="4ee0c-118">**Пример области с пошаговым представлением**</span><span class="sxs-lookup"><span data-stu-id="4ee0c-118">**Steps pane example**</span></span>

<img alt="A nonreactive web part with a steps pane property structure" src="../images/design-reactive-05.png" width="850">

## <a name="see-also"></a><span data-ttu-id="4ee0c-119">См. также</span><span class="sxs-lookup"><span data-stu-id="4ee0c-119">See also</span></span>

- [<span data-ttu-id="4ee0c-120">Разработка прекрасных решений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ee0c-120">Designing great SharePoint experiences</span></span>](design-guidance-overview.md)