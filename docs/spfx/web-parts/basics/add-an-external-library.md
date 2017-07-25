<span data-ttu-id="ee669-p123">Добавьте определения типов для строк. В этом случае у вас есть файл **MyStrings.d.ts**:</span><span class="sxs-lookup"><span data-stu-id="ee669-p123">Add typings for your strings. In this case, you have a file **MyStrings.d.ts**:</span></span>

```json
{
"strings": "strings/{locale}.js"
}
```
    
Добавьте определения типов для строк. В этом случае у вас есть файл **MyStrings.d.ts**:

```typescript
declare interface IStrings {
webpartTitle: string;
initialPrompt: string;
exitPrompt: string;
}

declare module 'mystrings' {
const strings: IStrings;
export = strings;
}
```
    
<span data-ttu-id="ee669-201">Добавьте операции импорта для строк в проекте:</span><span class="sxs-lookup"><span data-stu-id="ee669-201">Add imports for the strings in your project:</span></span>
    
```typescript
import * as strings from 'strings';
```
    
<span data-ttu-id="ee669-202">Используйте строки в своем проекте:</span><span class="sxs-lookup"><span data-stu-id="ee669-202">Use the strings in your project:</span></span>

```typescript
alert(strings.initialPrompt);
```
