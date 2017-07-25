<span data-ttu-id="220f7-p120">В редакторе кода откройте файл **./src/webparts/listInfo/ListInfoWebPart.ts**. Измените код метода **getPropertyPaneConfiguration** на такой:</span><span class="sxs-lookup"><span data-stu-id="220f7-p120">In the code editor open the **./src/webparts/listInfo/ListInfoWebPart.ts** file. Change the code of the **getPropertyPaneConfiguration** method to:</span></span>

В редакторе кода откройте файл **./src/webparts/listInfo/ListInfoWebPart.ts**. Измените код метода **getPropertyPaneConfiguration** на такой:

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
  // ...

  protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
    return {
      pages: [
        {
          header: {
            description: strings.PropertyPaneDescription
          },
          groups: [
            {
              groupName: strings.BasicGroupName,
              groupFields: [
                PropertyPaneTextField('description', {
                  label: strings.DescriptionFieldLabel,
                  onGetErrorMessage: this.validateDescription.bind(this)
                }),
                PropertyPaneTextField('listName', {
                  label: strings.ListNameFieldLabel,
                  onGetErrorMessage: this.validateListName.bind(this),
                  deferredValidationTime: 500
                })
              ]
            }
          ]
        }
      ]
    };
  }

  // ...
}

```

<span data-ttu-id="220f7-198">Свойство **deferredValidationTime** устанавливает длительность задержки перед запуском проверки SharePoint Framework (в миллисекундах).</span><span class="sxs-lookup"><span data-stu-id="220f7-198">The **deferredValidationTime** property specifies the number of milliseconds that the SharePoint Framework will wait before starting the validation process.</span></span>

<span data-ttu-id="220f7-199">Выполните следующую команду, чтобы проверить установленную задержку:</span><span class="sxs-lookup"><span data-stu-id="220f7-199">Run the following command to see that the applied delay is working as expected:</span></span>

```sh
gulp serve --nobrowser
```