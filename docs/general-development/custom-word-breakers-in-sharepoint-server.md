---
title: "Настраиваемые средства разбиения в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d18b48d4-987c-4228-9932-30d5b30f86a2
ms.openlocfilehash: 52ee69b816c55f49334d3309e10b331551284770
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="custom-word-breakers-in-sharepoint"></a><span data-ttu-id="178ca-102">Настраиваемые средства разбиения в SharePoint</span><span class="sxs-lookup"><span data-stu-id="178ca-102">Custom word breakers in SharePoint</span></span>
<span data-ttu-id="178ca-103">Узнайте о перенос слов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="178ca-103">Learn about word breaking in SharePoint.</span></span> <span data-ttu-id="178ca-104">Перенос слов является одним из ключевых функций обработки естественного языка (NLP), которые позволяют поиска и улучшить результаты поиска (или отзыва).</span><span class="sxs-lookup"><span data-stu-id="178ca-104">Word breaking is one of the key Natural Language Processing (NLP) features that enable search and improve search results (or recall).</span></span> <span data-ttu-id="178ca-105">Средства разбиения по словам разделение потока текста на отдельные слова или маркеров, на которых можно создать дополнительные языковые обработки.</span><span class="sxs-lookup"><span data-stu-id="178ca-105">Word breakers split a stream of text into individual words or tokens on which you can base additional language processing.</span></span> <span data-ttu-id="178ca-106">Средства разбиения по словам, зависящие от языка.</span><span class="sxs-lookup"><span data-stu-id="178ca-106">Word breakers are language-specific.</span></span> <span data-ttu-id="178ca-107">Кроме встроенных разбиения поиска в SharePoint позволяет использовать настраиваемые средства разбиения, чтобы пользователи могут настраивать поведение в соответствии с их требованиями перенос слов.</span><span class="sxs-lookup"><span data-stu-id="178ca-107">In addition to built-in word breakers, Search in SharePoint enables the use of custom word breakers so that users can tune word breaking behavior according to their needs.</span></span> <span data-ttu-id="178ca-108">Список языков, поддерживаемых для настройки средства разбиения слов в разделе [языки поддерживаются для настроек по словам word в SharePoint](#SP15_SupportedLanguages) .</span><span class="sxs-lookup"><span data-stu-id="178ca-108">See  [Supported languages for word breaker customizations in SharePoint](#SP15_SupportedLanguages) for a list languages supported for word breaker customization.</span></span>
  
    
    

<span data-ttu-id="178ca-109">Сведения о том, как писать средство разбиения по словам можно найти в следующих статьях</span><span class="sxs-lookup"><span data-stu-id="178ca-109">For information on how to write a word breaker refer to the following articles</span></span> 
-  [<span data-ttu-id="178ca-110">Реализация средства разбиения по словам</span><span class="sxs-lookup"><span data-stu-id="178ca-110">Implementing a Word Breaker</span></span>](http://msdn.microsoft.com/en-us/library/ms693186%28v=vs.85%29.aspx)
    
  
-  [<span data-ttu-id="178ca-111">Интерфейс IWordBreaker</span><span class="sxs-lookup"><span data-stu-id="178ca-111">IWordBreaker interface</span></span>](http://msdn.microsoft.com/en-us/library/ms691079%28v=vs.85%29.aspx)
    
  

## <a name="how-to-switch-to-a-custom-word-breaker-in-sharepoint"></a><span data-ttu-id="178ca-112">Как переключиться на настраиваемые слова в SharePoint</span><span class="sxs-lookup"><span data-stu-id="178ca-112">How to switch to a custom word breaker in SharePoint</span></span>
<span data-ttu-id="178ca-113"><a name="SP15wordbreaker_howto"> </a></span><span class="sxs-lookup"><span data-stu-id="178ca-113"></span></span>


> <span data-ttu-id="178ca-114">**Осторожность:** При замене существующего средства разбиения по словам редактора реестра на собственный риск.</span><span class="sxs-lookup"><span data-stu-id="178ca-114">**Caution:** When you replace existing word breakers, you modify the registry at your own risk.</span></span> <span data-ttu-id="178ca-115">Неправильное изменение реестра с помощью редактора реестра или другим способом могут возникнуть серьезные проблемы.</span><span class="sxs-lookup"><span data-stu-id="178ca-115">Serious problems might occur if you modify the registry incorrectly by using Registry Editor or by using another method.</span></span> <span data-ttu-id="178ca-116">Эти проблемы могут привести к переустановки операционной системы.</span><span class="sxs-lookup"><span data-stu-id="178ca-116">These problems might require that you reinstall the operating system.</span></span> <span data-ttu-id="178ca-117">Microsoft не удается убедитесь, что можно решить эти проблемы.</span><span class="sxs-lookup"><span data-stu-id="178ca-117">Microsoft cannot ensure that these problems can be solved.</span></span> <span data-ttu-id="178ca-118">Переключение на разных разбиения также может вызвать серьезные проблемы во время индексирования и обработки запросов.</span><span class="sxs-lookup"><span data-stu-id="178ca-118">Switching to a different word breaker might also cause serious problems during indexing and querying.</span></span> <span data-ttu-id="178ca-119">Перед изменением реестра резервное копирование реестра и убедитесь, что вы знаете, как для восстановления реестра в случае возникновения проблем.</span><span class="sxs-lookup"><span data-stu-id="178ca-119">Before you modify the registry, back up the registry and ensure that you know how to restore the registry if a problem occurs.</span></span> 
  
    
    

<span data-ttu-id="178ca-120">Выполните следующие действия, чтобы заменить существующие средства разбиения по словам настраиваемого разбиения или замените существующий средства разбиения по словам разбиения на другом языке.</span><span class="sxs-lookup"><span data-stu-id="178ca-120">Take the following steps to replace the existing word breaker with a custom word breaker or replace the existing word breaker with a word breaker in another language.</span></span>
  
    
    

1. <span data-ttu-id="178ca-121">Откройте редактор реестра, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="178ca-121">Open the Registry Editor, as follows:</span></span>
    
1. <span data-ttu-id="178ca-122">Выберите **Start**, а затем выберите **Run**.</span><span class="sxs-lookup"><span data-stu-id="178ca-122">Choose **Start**, and then choose **Run**.</span></span>
    
  
2. <span data-ttu-id="178ca-123">В диалоговом окне **Open** введите **Regedit** и нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="178ca-123">In the **Open** dialog box, type **Regedit**, and then choose **OK**.</span></span>
    
  
2. <span data-ttu-id="178ca-124">В редакторе реестра выберите следующий подраздел реестра:</span><span class="sxs-lookup"><span data-stu-id="178ca-124">In Registry Editor, select the following registry subkey:</span></span>
    
    <span data-ttu-id="178ca-125">**HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Office Server\\15.0\\Search\\Setup\\ContentIndexCommon\\LanguageResources\\Default\\** _language from the list below_</span><span class="sxs-lookup"><span data-stu-id="178ca-125">**HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Office Server\\15.0\\Search\\Setup\\ContentIndexCommon\\LanguageResources\\Default\\** _language from the list below_</span></span>
    
  
3. <span data-ttu-id="178ca-126">В правой области откройте контекстное меню для значения реестра **WBDLLPathOverride** и нажмите кнопку **Modify**.</span><span class="sxs-lookup"><span data-stu-id="178ca-126">In the right pane, open the shortcut menu for the **WBDLLPathOverride** registry value, and then choose **Modify**.</span></span>
    
  
4. <span data-ttu-id="178ca-p103">В диалоговом окне **Edit String** в поле **Value data** введите путь к вашей настраиваемого разбиения DLL-Библиотеку и выберите **OK**. Новую библиотеку DLL должен быть расположен в один и тот же путь как существующий файл DLL, который заменяется.</span><span class="sxs-lookup"><span data-stu-id="178ca-p103">In the **Edit String** dialog box, in the **Value data** box, type the path to your custom word breaker DLL, and then choose **OK**. The new DLL should be located in the same path as the existing DLL that is being replaced.</span></span>
    
  
5. <span data-ttu-id="178ca-129">В правой области откройте контекстное меню для значения реестра **WBreakerClass** и нажмите кнопку **Modify**.</span><span class="sxs-lookup"><span data-stu-id="178ca-129">In the right pane, open the shortcut menu for the **WBreakerClass** registry value, and then choose **Modify**.</span></span>
    
  
6. <span data-ttu-id="178ca-130">В диалоговом окне **Edit String** в поле **Value data** введите идентификатор класса вашего настраиваемого разбиения по словам и нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="178ca-130">In the **Edit String** dialog box, in the **Value data** box, type the class ID of your custom word breaker, and then choose **OK**.</span></span>
    
  
7. <span data-ttu-id="178ca-131">Перезапустите хост-контроллер поиска SharePoint и SharePoint.</span><span class="sxs-lookup"><span data-stu-id="178ca-131">Restart the SharePoint Search Host Controller and SharePoint.</span></span>
    
  
8. <span data-ttu-id="178ca-132">Выполните полный повторный обход.</span><span class="sxs-lookup"><span data-stu-id="178ca-132">Do a full re-crawl.</span></span>
    
  

## <a name="supported-languages-for-word-breaker-customizations-in-sharepoint"></a><span data-ttu-id="178ca-133">Поддерживаемые языки для настройки средства разбиения слов word в SharePoint</span><span class="sxs-lookup"><span data-stu-id="178ca-133">Supported languages for word breaker customizations in SharePoint</span></span>
<span data-ttu-id="178ca-134"><a name="SP15_SupportedLanguages"> </a></span><span class="sxs-lookup"><span data-stu-id="178ca-134"></span></span>

<span data-ttu-id="178ca-135">Для настройки средства разбиения слов word поддерживаются следующие языки:</span><span class="sxs-lookup"><span data-stu-id="178ca-135">The following languages are supported for word breaker customization:</span></span>
  
    
    
<span data-ttu-id="178ca-136">Арабский</span><span class="sxs-lookup"><span data-stu-id="178ca-136">Arabic</span></span>
  
    
    
<span data-ttu-id="178ca-137">Бенгальский</span><span class="sxs-lookup"><span data-stu-id="178ca-137">Bengali</span></span>
  
    
    
<span data-ttu-id="178ca-138">Болгарский</span><span class="sxs-lookup"><span data-stu-id="178ca-138">Bulgarian</span></span>
  
    
    
<span data-ttu-id="178ca-139">Каталанский</span><span class="sxs-lookup"><span data-stu-id="178ca-139">Catalan</span></span>
  
    
    
<span data-ttu-id="178ca-140">Китайский (Китайская Народная Республика)</span><span class="sxs-lookup"><span data-stu-id="178ca-140">Chinese (People's Republic of China)</span></span>
  
    
    
<span data-ttu-id="178ca-141">Китайский (Тайвань)</span><span class="sxs-lookup"><span data-stu-id="178ca-141">Chinese (Taiwan)</span></span>
  
    
    
<span data-ttu-id="178ca-142">Хорватский</span><span class="sxs-lookup"><span data-stu-id="178ca-142">Croatian</span></span>
  
    
    
<span data-ttu-id="178ca-143">Чешский</span><span class="sxs-lookup"><span data-stu-id="178ca-143">Czech</span></span>
  
    
    
<span data-ttu-id="178ca-144">Датский</span><span class="sxs-lookup"><span data-stu-id="178ca-144">Danish</span></span>
  
    
    
<span data-ttu-id="178ca-145">Нидерландский (голландский)</span><span class="sxs-lookup"><span data-stu-id="178ca-145">Dutch (Dutch)</span></span>
  
    
    
<span data-ttu-id="178ca-146">Английский (США)</span><span class="sxs-lookup"><span data-stu-id="178ca-146">English (United States)</span></span>
  
    
    
<span data-ttu-id="178ca-147">Эстонский</span><span class="sxs-lookup"><span data-stu-id="178ca-147">Estonian</span></span>
  
    
    
<span data-ttu-id="178ca-148">Финский</span><span class="sxs-lookup"><span data-stu-id="178ca-148">Finnish</span></span>
  
    
    
<span data-ttu-id="178ca-149">Французский (стандартный)</span><span class="sxs-lookup"><span data-stu-id="178ca-149">French (Standard)</span></span>
  
    
    
<span data-ttu-id="178ca-150">Немецкий (стандартный)</span><span class="sxs-lookup"><span data-stu-id="178ca-150">German (Standard)</span></span>
  
    
    
<span data-ttu-id="178ca-151">Греческий</span><span class="sxs-lookup"><span data-stu-id="178ca-151">Greek</span></span>
  
    
    
<span data-ttu-id="178ca-152">Гуджарати</span><span class="sxs-lookup"><span data-stu-id="178ca-152">Gujarati</span></span>
  
    
    
<span data-ttu-id="178ca-153">Иврит</span><span class="sxs-lookup"><span data-stu-id="178ca-153">Hebrew</span></span>
  
    
    
<span data-ttu-id="178ca-154">Хинди</span><span class="sxs-lookup"><span data-stu-id="178ca-154">Hindi</span></span>
  
    
    
<span data-ttu-id="178ca-155">Венгерский</span><span class="sxs-lookup"><span data-stu-id="178ca-155">Hungarian</span></span>
  
    
    
<span data-ttu-id="178ca-156">Исландский</span><span class="sxs-lookup"><span data-stu-id="178ca-156">Icelandic</span></span>
  
    
    
<span data-ttu-id="178ca-157">Индонезийский</span><span class="sxs-lookup"><span data-stu-id="178ca-157">Indonesian</span></span>
  
    
    
<span data-ttu-id="178ca-158">Итальянский (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="178ca-158">Italian (Default)</span></span>
  
    
    
<span data-ttu-id="178ca-159">Японский</span><span class="sxs-lookup"><span data-stu-id="178ca-159">Japanese</span></span>
  
    
    
<span data-ttu-id="178ca-160">Каннада</span><span class="sxs-lookup"><span data-stu-id="178ca-160">Kannada</span></span>
  
    
    
<span data-ttu-id="178ca-161">Казахский</span><span class="sxs-lookup"><span data-stu-id="178ca-161">Kazakh</span></span>
  
    
    
<span data-ttu-id="178ca-162">Корейский</span><span class="sxs-lookup"><span data-stu-id="178ca-162">Korean</span></span>
  
    
    
<span data-ttu-id="178ca-163">Латышский</span><span class="sxs-lookup"><span data-stu-id="178ca-163">Latvian</span></span>
  
    
    
<span data-ttu-id="178ca-164">Литовский</span><span class="sxs-lookup"><span data-stu-id="178ca-164">Lithuanian</span></span>
  
    
    
<span data-ttu-id="178ca-165">Малайский</span><span class="sxs-lookup"><span data-stu-id="178ca-165">Malay</span></span>
  
    
    
<span data-ttu-id="178ca-166">Малаялам</span><span class="sxs-lookup"><span data-stu-id="178ca-166">Malayalam</span></span>
  
    
    
<span data-ttu-id="178ca-167">Маратхи</span><span class="sxs-lookup"><span data-stu-id="178ca-167">Marathi</span></span>
  
    
    
<span data-ttu-id="178ca-168">Норвежский</span><span class="sxs-lookup"><span data-stu-id="178ca-168">Norwegian</span></span>
  
    
    
<span data-ttu-id="178ca-169">Польский</span><span class="sxs-lookup"><span data-stu-id="178ca-169">Polish</span></span>
  
    
    
<span data-ttu-id="178ca-170">Португальский (португальский)</span><span class="sxs-lookup"><span data-stu-id="178ca-170">Portuguese (Portuguese)</span></span>
  
    
    
<span data-ttu-id="178ca-171">Панджаби</span><span class="sxs-lookup"><span data-stu-id="178ca-171">Punjabi</span></span>
  
    
    
<span data-ttu-id="178ca-172">Румынский</span><span class="sxs-lookup"><span data-stu-id="178ca-172">Romanian</span></span>
  
    
    
<span data-ttu-id="178ca-173">Русский</span><span class="sxs-lookup"><span data-stu-id="178ca-173">Russian</span></span>
  
    
    
<span data-ttu-id="178ca-174">Сербский (кириллица)</span><span class="sxs-lookup"><span data-stu-id="178ca-174">Serbian (Cyrillic)</span></span>
  
    
    
<span data-ttu-id="178ca-175">Словацкий</span><span class="sxs-lookup"><span data-stu-id="178ca-175">Slovak</span></span>
  
    
    
<span data-ttu-id="178ca-176">Словенский</span><span class="sxs-lookup"><span data-stu-id="178ca-176">Slovenian</span></span>
  
    
    
<span data-ttu-id="178ca-177">Испанский (современная сортировка)</span><span class="sxs-lookup"><span data-stu-id="178ca-177">Spanish (Modern Sort)</span></span>
  
    
    
<span data-ttu-id="178ca-178">Шведский</span><span class="sxs-lookup"><span data-stu-id="178ca-178">Swedish</span></span>
  
    
    
<span data-ttu-id="178ca-179">Тамильский</span><span class="sxs-lookup"><span data-stu-id="178ca-179">Tamil</span></span>
  
    
    
<span data-ttu-id="178ca-180">Телугу</span><span class="sxs-lookup"><span data-stu-id="178ca-180">Telugu</span></span>
  
    
    
<span data-ttu-id="178ca-181">Тайский</span><span class="sxs-lookup"><span data-stu-id="178ca-181">Thai</span></span>
  
    
    
<span data-ttu-id="178ca-182">Турецкий</span><span class="sxs-lookup"><span data-stu-id="178ca-182">Turkish</span></span>
  
    
    
<span data-ttu-id="178ca-183">Украинский</span><span class="sxs-lookup"><span data-stu-id="178ca-183">Ukrainian</span></span>
  
    
    
<span data-ttu-id="178ca-184">Урду</span><span class="sxs-lookup"><span data-stu-id="178ca-184">Urdu</span></span>
  
    
    
<span data-ttu-id="178ca-185">Вьетнамский</span><span class="sxs-lookup"><span data-stu-id="178ca-185">Vietnamese</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="178ca-186">См. также</span><span class="sxs-lookup"><span data-stu-id="178ca-186">See also</span></span>
<span data-ttu-id="178ca-187"><a name="SP15wordbreakers_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="178ca-187"></span></span>


-  [<span data-ttu-id="178ca-188">Настройка службы поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="178ca-188">Configure search in SharePoint</span></span>](configure-search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="178ca-189">Реализация средства разбиения по словам</span><span class="sxs-lookup"><span data-stu-id="178ca-189">Implementing a Word Breaker</span></span>](http://msdn.microsoft.com/en-us/library/ms693186%28v=vs.85%29.aspx)
    
  
-  [<span data-ttu-id="178ca-190">Интерфейс IWordBreaker</span><span class="sxs-lookup"><span data-stu-id="178ca-190">IWordBreaker interface</span></span>](http://msdn.microsoft.com/en-us/library/ms691079%28v=vs.85%29.aspx)
    
  

