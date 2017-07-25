<span data-ttu-id="bbb71-p107">Хотя реактивного режима достаточно для многих сценариев, иногда требуется нереактивное поведение. В нереактивном режиме веб-часть не обновляется автоматически, если пользователь не подтвердит изменения.</span><span class="sxs-lookup"><span data-stu-id="bbb71-p107">While reactive mode is sufficient for many scenarios, at times you will need non-reactive behavior. Non-reactive does not update the web part automatically unless the user confirms the changes.</span></span>

Хотя реактивного режима достаточно для многих сценариев, иногда требуется нереактивное поведение. В нереактивном режиме веб-часть не обновляется автоматически, если пользователь не подтвердит изменения.

## <a name="custom-field-example"></a><span data-ttu-id="bbb71-146">Пример настраиваемого поля</span><span class="sxs-lookup"><span data-stu-id="bbb71-146">Custom field example</span></span>

<span data-ttu-id="bbb71-147">Добавьте следующее определение поля в массив **groupFields**:</span><span class="sxs-lookup"><span data-stu-id="bbb71-147">Add the following field definition in a **groupFields** array.</span></span>

```ts
{
  type: IPropertyPaneFieldType.Custom,
  targetProperty: 'custom',
  properties: {
    onRender: this._customFieldRender.bind(this),
    value: undefined,
    context: undefined
  }
}
```

<span data-ttu-id="bbb71-148">Добавьте следующие типы в импортированные элементы **@microsoft/sp-webpart-base**:</span><span class="sxs-lookup"><span data-stu-id="bbb71-148">Add the following types to the **@microsoft/sp-webpart-base** imports.</span></span>

```ts
IPropertyPaneFieldType
```

<span data-ttu-id="bbb71-149">Добавьте следующий частный метод для отрисовки настраиваемого поля:</span><span class="sxs-lookup"><span data-stu-id="bbb71-149">Add the following private method to render the custom field.</span></span>

```ts
private _customFieldRender(elem: HTMLElement, context: any, onChanged?: IOnCustomPropertyFieldChanged): void {
    elem.innerHTML = '<input id="password" type="password" name="password" class="ms-TextField-field">';
}
```
