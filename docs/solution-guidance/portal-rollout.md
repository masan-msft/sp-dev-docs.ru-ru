---
title: "Советы и рекомендации по развертыванию порталов SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: c4dddb0b318b64f3f04d51d5be85d3a6e2c10e40
ms.sourcegitcommit: 3276e9b281b227fb2f1a131ab4ac54ae212ce5cf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2017
---
# <a name="best-practices-for-rolling-out-sharepoint-online-portals"></a><span data-ttu-id="4a59e-102">Советы и рекомендации по развертыванию порталов SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="4a59e-102">Best practices for rolling out SharePoint Online portals</span></span>

<span data-ttu-id="4a59e-103">После уже долгое времени и энергии в здании, которое вы хотите, чтобы получить его портала на основе нового SharePoint live как можно скорее..., но бы хороший модели для этого?</span><span class="sxs-lookup"><span data-stu-id="4a59e-103">After you've spent your time and energy in building that new SharePoint based portal you do want to get it live as soon as possible...but what would be a good model for doing so?</span></span> <span data-ttu-id="4a59e-104">В этой статье будут рассмотрены следующие вопросы рекомендованной моделью развертывания портала для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="4a59e-104">This article will explain the recommended model for deploying your portal for your end users.</span></span>

><span data-ttu-id="4a59e-105">**Примечание**: несмотря на то, что данное руководство предназначен для SharePoint Online большая часть он также распространяется на порталов, размещенных в локальной среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4a59e-105">**Note**: Although this guidance is targeting SharePoint Online most of it also applies to portals hosted on a SharePoint on-premises environment.</span></span>


<span data-ttu-id="4a59e-106">_**Применимо к:** SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="4a59e-106">_**Applies to:** SharePoint Online_</span></span>

## <a name="anti-patterns-in-other-words-dont-do-these-things"></a><span data-ttu-id="4a59e-107">Защита от шаблонов (иными словами, не выполнить эти действия)</span><span class="sxs-lookup"><span data-stu-id="4a59e-107">Anti-patterns (in other words, don't do these things)</span></span>
<span data-ttu-id="4a59e-108"><a name="sectionSectionAntiPatterns"></a> Под списком содержит основных моментов, которые **не** делать, если речь идет о развертывании портал:</span><span class="sxs-lookup"><span data-stu-id="4a59e-108"><a name="sectionSectionAntiPatterns"> </a> Below list contains the key things **not** to do when it comes to rolling out your portal:</span></span>
- <span data-ttu-id="4a59e-109">Нагрузочное тестирование на портале с вашего клиента SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="4a59e-109">Stress test your portal against your SharePoint Online tenant</span></span>
- <span data-ttu-id="4a59e-110">Выполните знак предупреждения big выпуска, по сути отпускает новый портал для **всех** пользователей одновременно</span><span class="sxs-lookup"><span data-stu-id="4a59e-110">Do a big bang release, essentially releasing your new portal to **all** your users at the same moment</span></span>
- <span data-ttu-id="4a59e-111">Общий доступ к портал благодаря использованию большое число групп безопасности, как члены группы сайта может вызвать проблемы.</span><span class="sxs-lookup"><span data-stu-id="4a59e-111">Sharing your portal by having a large number of security groups as site group members can cause problems.</span></span> <span data-ttu-id="4a59e-112">Это может произойти с большим числом групп безопасности (30-40 КБ), каждый из которых членства в группе одного сайта, или она может быть несколько групп безопасности, которые являются членами многих групп сайта.</span><span class="sxs-lookup"><span data-stu-id="4a59e-112">This can happen with a large number (30-40K) security groups each with a single site group membership, or it can be a smaller number of security groups that are members of many site groups.</span></span>


## <a name="how-did-you-do-this-in-the-past"></a><span data-ttu-id="4a59e-113">Как вы сделали это в прошлом</span><span class="sxs-lookup"><span data-stu-id="4a59e-113">How did you do this in the past</span></span>
<span data-ttu-id="4a59e-114"><a name="sectionSection0"></a> Клиенты часто было запущено значительный испытания на их на локальном порталов SharePoint, как они хотели оценить ли инфраструктуры должны справиться с нагрузкой при этом сохраняя страницы приемлемое время загрузки.</span><span class="sxs-lookup"><span data-stu-id="4a59e-114"><a name="sectionSection0"> </a> Often customers did run massive stress tests on their SharePoint on-premises based portals as they wanted to assess whether the infrastructure would handle the load while still giving decent page load times.</span></span> <span data-ttu-id="4a59e-115">С помощью SharePoint Online тем не менее больше **не допускается выполнив классические нагрузочного тестирования** так как:</span><span class="sxs-lookup"><span data-stu-id="4a59e-115">With SharePoint Online however **doing a classical stress test is not allowed** anymore because:</span></span>
- <span data-ttu-id="4a59e-116">SharePoint Online будут видеть нагрузки тестирования как отказ в обслуживании и просто будет блокировать более того завершения клиента или пользователя</span><span class="sxs-lookup"><span data-stu-id="4a59e-116">SharePoint Online will see the load test as a denial of service attack and simply will block the user or even worse the complete tenant</span></span>
- <span data-ttu-id="4a59e-117">Если не блокируется нагрузочного теста будет возвращена, в результате чего серьезный интерпретировать результаты тестирования</span><span class="sxs-lookup"><span data-stu-id="4a59e-117">If the load test is not getting blocked it will be throttled resulting in hard to interpret test results</span></span>
- <span data-ttu-id="4a59e-118">SharePoint Online динамически масштабируются его базовой инфраструктуры, который отличный способ, но если вы не внезапно увеличение большой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4a59e-118">SharePoint Online will dynamically scale its underlying infrastructure which works great, but not if you suddenly do a massive load increase.</span></span> <span data-ttu-id="4a59e-119">Масштабирование модели серверной требуется время на выделить повышенной нагрузки</span><span class="sxs-lookup"><span data-stu-id="4a59e-119">The scaling back-end model needs time to absorb increased load</span></span>
- <span data-ttu-id="4a59e-120">Теста производительности — это просто одноразовый проверки в то время как вы портала будет хранить на развиваться, его лучше полагаться на встроенные портала телеметрии, чтобы вы можете постоянно исполнения на производительность портала.</span><span class="sxs-lookup"><span data-stu-id="4a59e-120">Such a performance test is just a one-time validation whereas you portal will keep on evolving ,it's better to rely on built in portal telemetry so that you're able to continuously follow-up on your portal performance.</span></span> <span data-ttu-id="4a59e-121">Также трудно построения нагрузочного теста, который представляет шаблон реальных об использовании.</span><span class="sxs-lookup"><span data-stu-id="4a59e-121">It's also hard to build a load test that represents a real usage pattern.</span></span>

<span data-ttu-id="4a59e-122">Рекомендуемый подход для развертывания нового портала с помощью поэтапный план развертывания в сочетании с встроенная портала телеметрии для измерения портала производительности при добавлении больше и больше пользователей.</span><span class="sxs-lookup"><span data-stu-id="4a59e-122">The recommended approach for rolling out your new portal is by using a phased roll-out plan combined with built in portal telemetry to measure portal performance while more and more users are added.</span></span> <span data-ttu-id="4a59e-123">Далее главы будет предоставлять получить дополнительные сведения о такой подход.</span><span class="sxs-lookup"><span data-stu-id="4a59e-123">The next chapter will provide more details around this approach.</span></span>

## <a name="recommendation-use-a-phased-portal-roll-out-strategy-combined-with-portal-telemetry"></a><span data-ttu-id="4a59e-124">Рекомендация: используйте поэтапный портала стратегии развертывания в сочетании с портала телеметрии</span><span class="sxs-lookup"><span data-stu-id="4a59e-124">Recommendation: use a phased portal roll-out strategy combined with portal telemetry</span></span>
<span data-ttu-id="4a59e-125">Часто используемые модель для развертывания новых возможностей использует поэтапный подход, который обычно состоит из:</span><span class="sxs-lookup"><span data-stu-id="4a59e-125">A commonly used model for rolling out new functionality is using a phased approach which typically consists of:</span></span>
- <span data-ttu-id="4a59e-126">**Пилотное** звукового файла: первый раз портала — это открыт для группы пользователей выбранного ключа.</span><span class="sxs-lookup"><span data-stu-id="4a59e-126">A **pilot** wave: this is the first time the portal is opened up to a group of selected key users.</span></span> <span data-ttu-id="4a59e-127">Очень важно для получения набора представитель, важных, ключевые пользователи, которые может предоставить первого свои отзывы и предложения</span><span class="sxs-lookup"><span data-stu-id="4a59e-127">It's important to get a set of representative, critical, key users that can provide the first feedback</span></span>
- <span data-ttu-id="4a59e-128">Один или несколько **конечных пользователей** этапами: зависит от числа этапами, у вас есть на какое число пользователей будет в сочетании с моделью вы создаете пример.</span><span class="sxs-lookup"><span data-stu-id="4a59e-128">One or more **end user** waves: the number of waves you have depends on how many users you'll be having combined with the model you're following.</span></span> <span data-ttu-id="4a59e-129">Мы видеть компаний, выравнивание их этапами развертывания с их структуры организации, других компаний выравнивание с country/region...in конечных самое, что имеет значение наиболее заключается в том, что постепенно добавляемым новых пользователей в портале</span><span class="sxs-lookup"><span data-stu-id="4a59e-129">We see companies aligning their roll-out waves with their organization structure, other companies are aligning by country/region...in the end the thing that matters most is the fact that you're gradually adding new users to the portal</span></span>

<span data-ttu-id="4a59e-130">Ниже рисунок показывает замечательно постепенного план развертывания.</span><span class="sxs-lookup"><span data-stu-id="4a59e-130">Below picture shows a nice gradual roll-out plan.</span></span> <span data-ttu-id="4a59e-131">Обратите внимание, что это также применяется в учетную запись, что обычно этапами конечных пользователей имеют меньше реальных пользователей выберите пригласить пользователей.</span><span class="sxs-lookup"><span data-stu-id="4a59e-131">Note that this also takes in account that typically end-user waves have less actual users then invited users.</span></span>

![поэтапный портала модель развертывания](https://support.content.office.net/en-us/media/0bc14a20-9420-4986-b9b9-fbcd2c6e0fb9.png)

<span data-ttu-id="4a59e-133">Время необходимо выделить свои отзывы и предложения и внести в портал при необходимости выше поэтапный подход, но как измерения и результатов по производительности в процессе это этапам развертывания?</span><span class="sxs-lookup"><span data-stu-id="4a59e-133">The above phased approach will give you time to absorb feedback and make adjustments to your portal if needed, but how do measure and follow-up on performance during this phased roll-out?</span></span> <span data-ttu-id="4a59e-134">Рекомендуемый подход для этого является внедрение портала телеметрии в реализации, как описано в [разделе телеметрии в статье производительности](https://msdn.microsoft.com/en-us/pnp_articles/portal-performance#telemetry).</span><span class="sxs-lookup"><span data-stu-id="4a59e-134">The recommended approach for doing this is embedding portal telemetry in your implementation, as explained in [telemetry section in performance article](https://msdn.microsoft.com/en-us/pnp_articles/portal-performance#telemetry).</span></span> <span data-ttu-id="4a59e-135">Наличие непрерывный поток данных портала производительности поможет вам понять, если портала производительности изменяется, когда растет число пользователей, а также когда вы в будущем сделать изменяется на портале.</span><span class="sxs-lookup"><span data-stu-id="4a59e-135">Having a continuous flow of portal performance data will help you understand if the portal performance is changing when the number of users is growing, but also when you in the future make changes to the portal.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a59e-136">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4a59e-136">Additional resources</span></span>
<span data-ttu-id="4a59e-137"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="4a59e-137"></span></span>

- [<span data-ttu-id="4a59e-138">Capacity planning and load testing SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="4a59e-138">Capacity planning and load testing SharePoint Online</span></span>](https://support.office.com/en-us/article/Capacity-planning-and-load-testing-SharePoint-Online-c932bd9b-fb9a-47ab-a330-6979d03688c0?ui=en-US&rs=en-US&ad=US)