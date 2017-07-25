<span data-ttu-id="61548-p105">_Только для чтения._ Возвращает значение этого объекта SPPermission.</span><span class="sxs-lookup"><span data-stu-id="61548-p105">_Read-only._ Returns the value of this SPPermission object</span></span> |
|`value`     | `public` | [`IODataBasePermission`](../sp-odata-types/iodatabasepermission.md) | _Только для чтения._ Возвращает значение этого объекта SPPermission. |
|`viewFormPages`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | <span data-ttu-id="61548-152">Просмотр форм, представлений и страниц приложений, а также перечисление списков.</span><span class="sxs-lookup"><span data-stu-id="61548-152">View forms, views, and application pages, and enumerate lists.</span></span> |
|`viewListItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | <span data-ttu-id="61548-153">Просмотр элементов в списках, а документов — в библиотеках документов, а также просмотр комментариев в веб-дискуссиях.</span><span class="sxs-lookup"><span data-stu-id="61548-153">View items in lists, documents in document libraries, and view Web discussion comments.</span></span> |
|`viewPages`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | <span data-ttu-id="61548-154">Просмотр страниц веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="61548-154">View pages in a Web site.</span></span> |
|`viewUsageData`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | <span data-ttu-id="61548-155">Просмотр отчетов об использовании веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="61548-155">View reports on Web site usage.</span></span> |
|`viewVersions`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | <span data-ttu-id="61548-156">Просмотр предыдущих версий элемента списка или документа.</span><span class="sxs-lookup"><span data-stu-id="61548-156">View past versions of a list item or document.</span></span> |




## <a name="methods"></a><span data-ttu-id="61548-157">Методы</span><span class="sxs-lookup"><span data-stu-id="61548-157">Methods</span></span>

| <span data-ttu-id="61548-158">Метод</span><span class="sxs-lookup"><span data-stu-id="61548-158">Method</span></span>       | <span data-ttu-id="61548-159">Модификатор доступа</span><span class="sxs-lookup"><span data-stu-id="61548-159">Access Modifier</span></span> | <span data-ttu-id="61548-160">Что возвращается</span><span class="sxs-lookup"><span data-stu-id="61548-160">Returns</span></span>  | <span data-ttu-id="61548-161">Описание</span><span class="sxs-lookup"><span data-stu-id="61548-161">Description</span></span>|
|:-------------|:----|:-------|:-----------|
|[`hasAllPermissions(...requestedPerms)`](hasallpermissions-sppermission.md)     | `public` | `boolean` | <span data-ttu-id="61548-162">Эта функция определяет, есть ли у заданной маски разрешений все запрашиваемые разрешения.</span><span class="sxs-lookup"><span data-stu-id="61548-162">Function for determining if a given permission mask has all of the requested permissions.</span></span> |
|[`hasAnyPermissions(...requestedPerms)`](hasanypermissions-sppermission.md)     | `public` | `boolean` | <span data-ttu-id="61548-163">Эта функция определяет, есть ли у заданной маски разрешений какое-либо из запрашиваемых разрешений.</span><span class="sxs-lookup"><span data-stu-id="61548-163">Function for determining if a given permission mask has any of the requested permissions.</span></span> |
|[`hasPermission(requestedPerm)`](haspermission-sppermission.md)     | `public` | `boolean` | <span data-ttu-id="61548-164">Эта функция проверяет, есть ли у заданной маски разрешений запрашиваемое разрешение.</span><span class="sxs-lookup"><span data-stu-id="61548-164">Function for checking if a given permission mask has the requested permission.</span></span> |





