<span data-ttu-id="27f22-p107"><a name="bk_folders"> </a> Служба REST SharePoint не поддерживает переход по иерархии папок сайта путем составления URL-адресов. Вместо этого можно использовать аналог метода **Web.GetFolderByServerRelativeUrl** в службе REST. Например:</span><span class="sxs-lookup"><span data-stu-id="27f22-p107"><a name="bk_folders"> </a> The SharePoint REST service does not support traversing the folder hierarchy of a site through the URL construction. Instead, use the REST equivalent of the  **Web.GetFolderByServerRelativeUrl** method. For example:</span></span>
<a name="bk_folders"> </a> Служба REST SharePoint не поддерживает переход по иерархии папок сайта путем составления URL-адресов. Вместо этого можно использовать аналог метода **Web.GetFolderByServerRelativeUrl** в службе REST. Например:
 
 <span data-ttu-id="27f22-137">*Навигация, не поддерживаемая в службе REST:*</span><span class="sxs-lookup"><span data-stu-id="27f22-137">*Navigation not supported through the REST service:*</span></span> 
  
 `/_vti_bin/client.svc/web/lists/SharedDocuments/folder1/stuff/things/Recycle`
 
<span data-ttu-id="27f22-138">Навигация, поддерживаемая в службе REST:</span><span class="sxs-lookup"><span data-stu-id="27f22-138">Navigation that is supported by the REST service:</span></span> 
 
 <span data-ttu-id="27f22-139">`/_vti_bin/client.svc/web/GetFolderByServerRelativeUrl('SharedDocuments/folder1/stuff/things')/Recycle`.</span><span class="sxs-lookup"><span data-stu-id="27f22-139"></span></span>
 

## <a name="spcontextwebinformation-object-properties"></a><span data-ttu-id="27f22-140">Свойства объекта SPContextWebInformation</span><span class="sxs-lookup"><span data-stu-id="27f22-140">SPContextWebInformation object properties</span></span>
<span data-ttu-id="27f22-141"><a name="bk_props"> </a></span><span class="sxs-lookup"><span data-stu-id="27f22-141"></span></span>

|<span data-ttu-id="27f22-142">**Свойство SPContextWebInformation**</span><span class="sxs-lookup"><span data-stu-id="27f22-142">**SPContextWebInformation Property**</span></span>|<span data-ttu-id="27f22-143">**Описание**</span><span class="sxs-lookup"><span data-stu-id="27f22-143">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="27f22-144">**webFullUrl**</span><span class="sxs-lookup"><span data-stu-id="27f22-144">**webFullUrl**</span></span>|<span data-ttu-id="27f22-145">Возвращает URL-адрес относительно сервера для ближайшего сайта.</span><span class="sxs-lookup"><span data-stu-id="27f22-145">Gets the server-relative URL of the nearest site.</span></span>|
|<span data-ttu-id="27f22-146">**siteFullUrl**</span><span class="sxs-lookup"><span data-stu-id="27f22-146">**siteFullUrl**</span></span>|<span data-ttu-id="27f22-147">Возвращает URL-адрес относительно сервера для корня семейства веб-сайтов, включающего текущий сайт. Если ближайший веб-сайт является корнем семейства веб-сайтов, значение свойства **webFullUrl** будет совпадать со значением свойства **siteFullUrl**.</span><span class="sxs-lookup"><span data-stu-id="27f22-147">Gets the server-relative URL of the root of the site collection that the site is contained within.If the nearest web is the root of a site collection, then the value of the  **webFullUrl** property is equal to the **siteFullUrl** property.</span></span>|
|<span data-ttu-id="27f22-148">**formDigestValue**</span><span class="sxs-lookup"><span data-stu-id="27f22-148">**formDigestValue**</span></span>|<span data-ttu-id="27f22-149">Возвращает дайджест формы запроса сервера.</span><span class="sxs-lookup"><span data-stu-id="27f22-149">Gets the server's request form digest.</span></span>|
|<span data-ttu-id="27f22-150">**LibraryVersion**</span><span class="sxs-lookup"><span data-stu-id="27f22-150">**LibraryVersion**</span></span>|<span data-ttu-id="27f22-151">Возвращает текущую версию библиотеки REST.</span><span class="sxs-lookup"><span data-stu-id="27f22-151">Gets the current version of the REST library.</span></span>|
|<span data-ttu-id="27f22-152">**SupportedSchemaVersions**</span><span class="sxs-lookup"><span data-stu-id="27f22-152">**SupportedSchemaVersions**</span></span>|<span data-ttu-id="27f22-153">Получает поддерживаемые версии схемы библиотеки REST/CSOM.</span><span class="sxs-lookup"><span data-stu-id="27f22-153">Gets the versions of the schema of the REST/CSOM library that are supported.</span></span>|

## <a name="webinfo-object"></a><span data-ttu-id="27f22-154">Объект WebInfo</span><span class="sxs-lookup"><span data-stu-id="27f22-154">WebInfo object</span></span>
<span data-ttu-id="27f22-155"><a name="bk_webinfo"> </a></span><span class="sxs-lookup"><span data-stu-id="27f22-155"></span></span>

|<span data-ttu-id="27f22-156">**Свойство WebInfo**</span><span class="sxs-lookup"><span data-stu-id="27f22-156">**WebInfo property**</span></span>|<span data-ttu-id="27f22-157">**Описание**</span><span class="sxs-lookup"><span data-stu-id="27f22-157">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="27f22-158">**Created**</span><span class="sxs-lookup"><span data-stu-id="27f22-158">**Created**</span></span>|<span data-ttu-id="27f22-159">Возвращает значение, определяющее, когда был создан сайт.</span><span class="sxs-lookup"><span data-stu-id="27f22-159">Gets a value that specifies when the site was created.</span></span>|
|<span data-ttu-id="27f22-160">**Description**</span><span class="sxs-lookup"><span data-stu-id="27f22-160">**Description**</span></span>|<span data-ttu-id="27f22-161">Возвращает или задает описание сайта.</span><span class="sxs-lookup"><span data-stu-id="27f22-161">Gets or sets the description for the site.</span></span>|
|<span data-ttu-id="27f22-162">**Id**</span><span class="sxs-lookup"><span data-stu-id="27f22-162">**Id**</span></span>|<span data-ttu-id="27f22-163">Возвращает значение, указывающее идентификатор сайта.</span><span class="sxs-lookup"><span data-stu-id="27f22-163">Gets a value that specifies the site identifier.</span></span>|
|<span data-ttu-id="27f22-164">**Language**</span><span class="sxs-lookup"><span data-stu-id="27f22-164">**Language**</span></span>|<span data-ttu-id="27f22-165">Возвращает значение, указывающее код языка, используемого на сайте.</span><span class="sxs-lookup"><span data-stu-id="27f22-165">Gets a value that specifies the locale ID (LCID) for the language that is used on the site.</span></span>|
|<span data-ttu-id="27f22-166">**LastItemModifiedDate**</span><span class="sxs-lookup"><span data-stu-id="27f22-166">**LastItemModifiedDate**</span></span>|<span data-ttu-id="27f22-167">Возвращает значение, определяющее, когда в последний раз был изменен элемент на сайте.</span><span class="sxs-lookup"><span data-stu-id="27f22-167">Gets a value that specifies when an item was last modified in the site.</span></span>|
|<span data-ttu-id="27f22-168">**Title**</span><span class="sxs-lookup"><span data-stu-id="27f22-168">**Title**</span></span>|<span data-ttu-id="27f22-169">Получает или задает название сайта.</span><span class="sxs-lookup"><span data-stu-id="27f22-169">Gets or sets the title for the site.</span></span>|
|<span data-ttu-id="27f22-170">**WebTemplateId**</span><span class="sxs-lookup"><span data-stu-id="27f22-170">**WebTemplateId**</span></span>|<span data-ttu-id="27f22-171">Получает идентификатор шаблона сайта.</span><span class="sxs-lookup"><span data-stu-id="27f22-171">Gets the identifier of the site template.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="27f22-172">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="27f22-172">Additional resources</span></span>
<span data-ttu-id="27f22-173"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="27f22-173"></span></span>

-  [<span data-ttu-id="27f22-174">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="27f22-174">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
-  [<span data-ttu-id="27f22-175">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="27f22-175">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="27f22-176">Работа со списками и элементами списков в интерфейсе REST</span><span class="sxs-lookup"><span data-stu-id="27f22-176">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
-  [<span data-ttu-id="27f22-177">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="27f22-177">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
-  [<span data-ttu-id="27f22-178">Определение URI для конечных точек службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="27f22-178">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris.md)
-  [<span data-ttu-id="27f22-179">Использование операций запросов OData в запросах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="27f22-179">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests.md)
-  [<span data-ttu-id="27f22-180">Справочные материалы и примеры по REST API</span><span class="sxs-lookup"><span data-stu-id="27f22-180">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [<span data-ttu-id="27f22-181">Синхронизация элементов SharePoint с помощью службы REST</span><span class="sxs-lookup"><span data-stu-id="27f22-181">Synchronize SharePoint items using the REST service</span></span>](synchronize-sharepoint-items-using-the-rest-service.md)
-  [<span data-ttu-id="27f22-182">Получение версий элементов списков и документов с помощью значений ETag в службе REST</span><span class="sxs-lookup"><span data-stu-id="27f22-182">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/use-etag-values-through-the-rest-service-to-get-document-list-item-versioning%28Office.15%29.aspx)
    
 

 

 

